<template>
    <div>
        <section class="main">
            <div class="inner">
                <img src="logo-expanded.svg" alt="Logo completo">
                <img :src="data.home_image" alt="">
                <article class="content">
                    <Content />
                    <h1>{{data.mission}}</h1>
                </article>
            </div>
        </section>

        <section class="profile">
            <div class="inner row">
                <div class="column">
                    <article class="avatar">
                        <img :src="data.avatar" />
                    </article>
                    <h1>{{data.name}}</h1>

                    <article class="description">
                        {{data.profile_text}}
                    </article>
                </div>
                <div class="column products">

                    <div class="logos">
                        <a v-for="product in data.products" :href="product.url">
                            <img :src="product.logo">
                        </a>
                    </div>
                    <p>{{data.products_text}}</p>
                </div>
            </div>

            <div class="inner row">
                <ClientOnly>
                    <div class="gallery">
                        <img :class="'area-'+i" v-for="(image, i) in data.gallery.slice(0, 3)" :src="image" @click="update(i)">
                    </div>
                    <VueGallerySlideshow ref="lightbox" :images="data.gallery" :index="index" @close="update(null)"></VueGallerySlideshow>
                </ClientOnly>
            </div>
        </section>
        <section class="contacts">
            <article class="contacts">
                <h1 id="contacts">Contatti</h1>
            </article>
            <img src="maubg.png" alt="Maurizio Fabbri" class="img-responsive">
            <article class="contacts">
                <p>
                    <p>
                        <img src="phone.svg" alt="">&nbsp;
                        <a href="tel:+390542643314">
                            +39 0542 643314
                        </a>
                    </p>
                    <p>
                        <img src="mail.svg" alt="">&nbsp;
                        <a href="mailto:studiomparrucchieri@gmail.com">
                            studiomparrucchieri@gmail.com
                        </a>
                    </p>
                    <p>
                        <img src="map-pin.svg" alt="">&nbsp;
                        <a href="https://www.google.it/maps/place/Studio+M+Di+Fabbri+Maurizio/@44.3771006,11.7263129,15z/data=!4m5!3m4!1s0x0:0x346d6bb38e4702a6!8m2!3d44.3771006!4d11.7263129">
                            Torre Lasie, via Lasie 10/L
                            40026 Imola
                        </a>
                    </p>
                </p>
            </article>
            <article class="times">
                <h1>Orari</h1>
                <div>
                    <div>da&nbsp;</div>
                    <div>{{data.times}}</div>    
                </div>
            </article>
            <article class="social">
                <a href="https://www.facebook.com/pg/Studio-M-Parrucchieri-1644568429132611/photos/?ref=page_internal">
                    <div>
                        <img src="facebook.svg" alt="">
                    </div>
                </a>
                <a href="https://www.instagram.com/studiomparrucchieri/">
                    <div>
                        <img src="instagram.svg" alt="">
                    </div>
                </a>
            </article>
        </section>
        <section class="map">
            <div class="map-container">
                <Map />
            </div>
        </section>
    </div>
</template>

<script>
export default {
  computed: {
    data() {
        return this.$page.frontmatter;
    }
  },
  data() {
    return {
        index: null
    }
  },
  methods: {
    update: function(event) {
        this.index = event;
    }
  }
};
</script>

<style lang="scss">
article.content {
    line-height: 1.2rem;

    p + p {
        margin-top: 1rem;
    }

    h1 {
        line-height: 1.2;
    }
}

</style>


<style lang="scss" scoped>
section {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: auto;
    padding-bottom: 3rem;

    @media screen and (min-width: 600px) {
        justify-content: center;
    }

    .inner {
        margin: 0 1rem;

        @media screen and (min-width: 600px) {
            max-width: 66vw;
            margin: auto;
        }
    }
}

h1,
h2 {
    font-family: 'Oswald';
    font-weight: 200;
    text-transform: uppercase;
    margin: auto;
    display: block;
    text-align: center;
    margin: 2rem 0;
    font-size: 2em;
}

img {
    display: block;
    margin: auto;
    max-width: 100%;
}

.main {
    article {
        margin: 2rem;
    }

    img + img {
        margin: 2rem auto;
    }

}

.profile {
    background: white;
    color: black;
    padding: 2rem 0;

    padding-bottom: 3rem;
    position: relative;
    &:before {
        content: '';
        position: absolute;
        top: -1rem;
        @media screen and (min-width: 600px) {
            top: -3rem;
        }
        left: 0;
        right: 0;
        height: 6rem;
        background: white;
        transform: skewY(2deg);
        z-index: -1;
    }

    &:after {
        content: '';
        position: absolute;
        bottom: -1rem;
        @media screen and (min-width: 600px) {
            bottom: -3rem;
        }
        left: 0;
        right: 0;
        height: 6rem;
        background: white;
        transform: skewY(2deg);
        z-index: 2;
    }

    .avatar {
        img {
            max-width: 100%;
        }
    }

    .description {
        margin: 1rem;
    }

    + * {
        position: relative;
        z-index: 1;
    }
}

.row {
    display: flex;
    flex-direction: column;
    align-items: center;

    @media screen and (min-width: 1024px) {
        flex-direction: row;
    }

    .column {
        flex: 1;

        + .column {
            margin-top: 3rem;

            @media screen and (min-width: 1024px) {
                margin-top: 0;
                margin-left: 3rem;
            }
        }
    }
}

.products {
    display: flex;
    flex-direction: column-reverse;

    @media screen and (min-width: 1024px) {
        flex-direction: column;
    }

    .logos {
        margin: 2rem 4rem;

        a {
            display: block;
        }

        > * + * {
            margin-top: 2rem;
        }
    }

    p {
        text-align: center;
    }
}

section.contacts {
    margin-top: 6rem;
    display: flex;
    justify-content: center;
    position: relative;
    z-index: 2;

    h1 {
        margin: auto;
    }

    > * {
        width: 95vw;
        margin: 1.2rem auto 0 auto;

        @media screen and (min-width: 1024px) {
            width: auto;
        }
    }

    img {
        width: 75vw;
        @media screen and (min-width: 1024px) {
            width: 50vw;
        }
    }

    &:after {
        content: '';
        position: absolute;
        bottom: -2rem;
        @media screen and (min-width: 600px) {
            bottom: -3rem;
        }
        left: 0;
        right: 0;
        height: 6rem;
        background: black;
        transform: skewY(2deg);
        z-index: -1;
    }

     .contacts {            
        a {
            display: inline-block;
            position: relative;
            line-height: 1.4rem;
            margin-bottom: 0.2rem;

            border-bottom: 2px solid white;
            transition: border 150ms ease-in-out;

            &:hover {
                border-bottom: 2px solid transparent;
            }
        }
    }

    article {
        img {
            width: 1em;
            height: 1em;
            display: inline;
            margin: auto;
        }
    }

    .social {
    display: flex;
    justify-content: flex-end;
    margin-top: 2rem;

        > *, img {
            height: 3rem;
            width: 3rem;

            + * {
                margin-left: 1.5rem;
            }
        }
    }
}

.map {
    flex-direction: column-reverse;
    display: flex;
    padding: 0;
    margin: 0;
    height: 66vh;
    position: relative;
    z-index: 1;

    &-container {
        height: 100%;
        width: 100%;
    }

    @media screen and (min-width: 600px) {
        flex-direction: row;
        width: 100%;
        min-height: 700px;
    }
    
}

.times {
    > div {
        display: flex;
    }

    white-space: pre-line;

    h1 {
        text-align: left;
    }
}

.gallery {
  margin: 2rem;
  display: grid;
  height: 100%;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 1fr 1fr;
  grid-template-areas: "area-0 area-0" "area-1 area-2";
  grid-gap: 1em;

    @media screen and (min-width: 600px) {
        grid-template-columns: 2fr 1fr 1fr;
        grid-template-rows: 1fr;
        grid-template-areas: "area-0 area-1 area-2";
        grid-gap: 0px 1em;
    }
}
.area-0 { grid-area: area-0; }

.area-1 { grid-area: area-1; }

.area-2 { grid-area: area-2; }

.area-3 { grid-area: area-3; }

.area-4 { grid-area: area-4; }

</style>