<template>
    <div class="outerWrapper">
        <div class="innerWrapper">
            <div class="photo">
                <img :src="photo">
            </div>
            <div class="description">
                <h2 class="title">Author:  {{title}}</h2>
                <p class="description">
                   To see the source click button below
                </p>
                <div class="button-wrapper">
                    <a :href="description" target="_blank"><button type="button" >Click Me!</button></a>
                </div>
            </div>
        </div>
        <div class="close" @click="$emit('closemodal')"/>
    </div>
</template>

<script>
export default {
  name: 'Modal',
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      photo: null,
      title: null,
      description: null,
    };
  },
  mounted() {
    this.photo = this.item.largeImageURL;
    this.title = this.item.user;
    this.description = this.item.pageURL;
  },
};
</script>

<style lang="scss" scoped>
    .outerWrapper {
        background: #f6f6f6;
        max-width: 100%;
        height: 80%;
        position: fixed;
        top: 0;
        left: 0;

        @media (min-width: 1024px) {
            max-width: 80%;
            height: 55%;
            left: 0;
            right: 0;
            top: 0;
            bottom: 0;
            margin: auto;
            box-shadow: 0 30px 30px -10px rgba(0,0,0, .3);
        }

        @media (min-width: 1600px) {
            height: 70%;
        }
    }

    .close {
        position: absolute;
        width: 30px;
        height: 30px;
        padding: 30px;
        right: 0;
        top: 0;
        cursor: pointer;

        &::before,
        &::after {
            position: absolute;
            content: '';
            top: 30px;
            right: 20px;
            width: 20px;
            height: 2px;
            background: black;
            display: block;
        }

        &::before {
            transform: rotate(45deg);
        }
        &::after {
            transform: rotate(-45deg);
        }
    }

    .innerWrapper {
        display: flex;
        height: 100%;
        padding: 5px;
        margin-left: 0px;
        justify-content: center;
        align-items: center;
        flex-direction: column;

        @media (min-width: 1024px) {
            flex-direction: row;

            .photo {
                width: 122%;
                margin-right: 20px;
                margin-left: -40px;
            }
        }

        @media (min-width: 1600px) {
            .photo {
                width: 77%;
            }
        }

        .photo {
            max-width: 100%;
            height: auto;
            background: black;

            img {
                width: 100%;
            }
        }

        .description {
            color: #333;
            max-width: 400px;

            .button-wrapper {
                display: flex;
                justify-content: center;
                margin-top: 20px;
            }

            button {
                width: 100px;
                height: 40px;
                font-weight: 400;
                text-align: center;
                background-color: #333;
                color: white;
                border-radius: 17px;
                    font-family: 'Montserrat', sans-serif;
            }
        }

        .title {
            color: #1e3d4a;
        }

    }

</style>
