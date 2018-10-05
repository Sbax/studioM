<template>
    <div>
        <section class="main">
            <div class="inner">
                <img src="logo-expanded.svg" alt="Logo completo">
                <article>
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
                        {{data.info}}
                    </article>
                </div>
                <div class="column products">

                    <div class="logos">
                        <a href="https://www.wella.com/professional/it-IT/home"><img src="wella-logo-black.png" alt="Wella"></a>
                        <a href="https://it.tigiprofessional.com/?country=IT"><img src="tigi-logo-black.png" alt="Tigi"></a>
                        <a href="https://terradisole.it/"><img src="terradisole-logo-black.png" alt="Terra di Sole"></a>
                    </div>
                    <p>Lo studio M si affida all'esperienza e professionalità delle migliori case di cosmetici per la bellezza e salute dei tuoi capelli.</p>
                </div>
            </div>
        </section>
        <section class="map">
            <div class="column">
                <Map />
            </div>
            <div class="column">
                <div class="times">
                    Aperto da martedì a giovedì dalle 12 alle 19,30<br>
                    venerdì dalle 9 alle 19<br>
                    sabato dalle 9 alle 17<br>
                </div>
                <div class="place">
                    Torre Lasie - via Lasie 10/L<br>
                    40026 Imola (Bo)<br>
                    +39 0542 643314<br>
                    studiomparrucchieri@gmail.com
                </div>
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
  }
};
</script>

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

.map {
    flex-direction: row;
    display: flex;
    padding: 0;
    width: 100%;
    height: 66vh;

    .column {
        flex: 1;
        height: 100%;
        background: black;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }
}
</style>