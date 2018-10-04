<template>
  <section class="news">
    <article v-for="item in items">
      <h2 v-html="item.title"></h2>
      <h4>{{item.date}}</h4>
      <p v-html="item.content"></p>
    </article>
  </section>
</template>

<script>
const axios = require('axios')
export default {
  data () {
    return {
      items: []
    }
  },
  async beforeMount() {
    const sessionNews = JSON.parse(sessionStorage.getItem("news"));
    
    const response = sessionNews || (await axios.get('https://public-api.wordpress.com/wp/v2/sites/studiomparrucchierinews.wordpress.com/posts'));
    
    sessionStorage.setItem("news", JSON.stringify(response));

    this.$data.items = response.data.map((e, i) => {
      const content = document.createElement('p');
      content.innerHTML = e.content.rendered;

      const slideshow = [];

      [...content.querySelectorAll(".gallery")]
        .map((gallery, index) => {
          [...gallery.querySelectorAll('a')]
            .map(link => link.removeAttribute('href'));
          
          return gallery;
        });

      return {
        count: i,
        date: new Date().toLocaleDateString('it', {
          day: 'numeric',
          month: 'long',
          year: 'numeric'
        }),
        title: e.title.rendered,
        content: content.innerHTML,
      }
    });

  },
  updated() {
    
  }
}
</script>

<style lang="scss">
.news {
    .gallery {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;

        > * {
            display: flex;
            justify-content: center;
            align-items: center;
            margin: 1rem;
        }
    }

    h1,
    h2 {
        font-size: 2em;
        font-weight: 400;
        font-family: 'Oswald';
        margin: 0.5rem;
        text-transform: uppercase;
        line-height: 1.1em;
    }

    h4 {
        font-size: 1.2em;
        font-weight: 300;
        font-family: 'Oswald';
        margin: 1rem;
        margin-top: 0;
        text-transform: uppercase;
    }

    p {
        margin-bottom: 2rem;
    }

    @media screen and (min-width: 600px) {
        max-width: 60vw;
        margin: auto;
    }

    article {
        font-weight: 100;
        line-height: 1.4rem;
        margin-top: 2rem;
        padding: 1rem;
        &:nth-child(even) {
            background: white;
            color: black;

            position: relative;
            &:before {
                content: '';
                position: absolute;
                top: -1.5rem;
                left: 0;
                right: 0;
                height: 6rem;
                z-index: -1;
                background: white;
                transform: skewY(2deg);
            }

            &:not(:last-child):after {
                content: '';
                position: absolute;
                bottom: -1rem;
                left: 0;
                right: 0;
                height: 6rem;
                z-index: -1;
                background: white;
                transform: skewY(2deg);
            }
        }
    }
}
</style>
