<template>
    <header>
        <div class="logo-container">
            <router-link to="/">
                <img class="logo" :src="logo" :alt="$site.title">
            </router-link>
        </div>

        <nav v-if="navLinks">
            <ul class="desktop-nav">
                <router-link v-for="nav in navLinks" :key="nav.text" tag="li" :to="nav.link" active-class="active" v-text="nav.text" exact />
            </ul>
        </nav>
    </header>
</template>

<script>
export default {
    props: {
        logo: {
            type: String,
            required: false
        }
    },
    computed: {
        navLinks() {
            return this.$site.themeConfig.nav;
        }
    }
};
</script>


<style lang="scss" scoped>
.desktop-nav {
    display: flex;
}

.logo {
    max-width: 100%;
    max-height: 4rem;

    &-container {
        display: flex;
        align-items: center;
    }
}

$navbar-height: 6rem;

header {
    font-family: 'Oswald', sans-serif;
    font-size: 1.2rem;
    text-transform: uppercase;
    font-weight: 200;
    height: $navbar-height;
    display: flex;
    justify-content: space-between;
    align-items: stretch;
    padding: 1rem 1.5rem;

    ul {
        display: flex;
        list-style-type: none;
        height: 100%;
        li {
            min-width: $navbar-height;
            height: 100%;
            margin: 0;
            display: flex;
            align-items: center;
            justify-content: center;

            cursor: pointer;
            position: relative;
            overflow: hidden;

            &:before {
                content: '';
                position: absolute;
                left: 10%;
                bottom: 0.5rem;
                width: 80%;
                height: 2px;
                background: white;
                transform: scaleX(0);
                transition: transform 300ms ease;
            }

            &:hover,
            &.active {
                &:before {
                    transform: scaleX(1);
                }
            }

            &.active {
                cursor: default;
                opacity: 0.5;
            }
        }
    }
}
</style>