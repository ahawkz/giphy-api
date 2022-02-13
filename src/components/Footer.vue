<template>
    <footer>
         <p>
             <a href="https://www.alexhawkins.dev/" target="_blank">You don't know about me, but I bet you want to</a>
             <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><!--! Font Awesome Pro 6.0.0 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. --><path d="M502.6 278.6l-128 128c-12.51 12.51-32.76 12.49-45.25 0c-12.5-12.5-12.5-32.75 0-45.25L402.8 288H32C14.31 288 0 273.7 0 255.1S14.31 224 32 224h370.8l-73.38-73.38c-12.5-12.5-12.5-32.75 0-45.25s32.75-12.5 45.25 0l128 128C515.1 245.9 515.1 266.1 502.6 278.6z"/></svg>
         </p>
    </footer>
</template>

<script>
export default ({
    name: 'Footer'
})
</script>

<style scoped lang="scss">
@import "../scss/_variables.scss";
@import "../scss/_typography.scss";

footer {
    flex-shrink: 0;
    padding-bottom: 10px;

    p {
        display: flex;
        align-items: center;
        justify-content: center;
        a {
            color: $red;
            letter-spacing: 0.5px;
            font-family: $secondary-font;
            text-decoration: none;
            &:hover {
                text-decoration: underline;
            }
        }
        svg {
            height: 100%;
            width: 20px;
            fill: $red;
            margin: 0 10px;
        }
        &:hover svg {
            transform: translateX(20%);
            transition: 0.3s all;
        }
    }
}


</style>
