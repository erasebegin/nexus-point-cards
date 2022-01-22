<template>
  <div class="card-container">
    <div class="card-top">
      <div class="image-top">
        <span class="classification">{{
          car.advert_classification | capitalise
        }}</span>
        <div class="button-container">
          <p>{{ `${currentImage + 1} of ${car.media_urls.length}` }}</p>
          <button @click="decrement">
            <img src="../assets/left.svg" alt="left arrow" />
          </button>
          <button @click="increment">
            <img src="../assets/right.svg" alt="right arrow" />
          </button>
        </div>
      </div>
      <div class="tags">
        <p
          v-for="(feature, index) in car.feature_classification[0].slice(0, 3)"
          :key="index"
        >
          {{ feature }}
        </p>
      </div>
      <img
        :src="car.media_urls[currentImage].thumb"
        class="card-image"
        :alt="car.name"
      />
    </div>
    <div class="card-bottom">
      <div class="title-container">
        <div class="title-left">
          <h3>{{ car.name }}</h3>
          <p>{{ car.derivative }}</p>
        </div>
        <img
          src="../assets/star-outline.svg"
          v-if="!isStarred"
          @click="toggle"
        />
        <img src="../assets/star-fill.svg" v-if="isStarred" @click="toggle" />
      </div>
      <p class="price">£{{ Math.round(car.price) }}</p>
      <p class="price-when-new">
        £{{ car.price_when_new }}
        <a href="www.google.com" class="calculate-link">Calculate finance</a>
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: {
    car: Object,
  },
  data() {
    return { isStarred: false, currentImage: 0 };
  },
  methods: {
    toggle() {
      this.isStarred = !this.isStarred;
    },
    increment() {
      if (this.currentImage < this.car.media_urls.length - 1) {
        this.currentImage += 1;
      } else {
        this.currentImage = 0;
      }
    },
    decrement() {
      if (this.currentImage > 0) {
        this.currentImage -= 1;
      } else {
        this.currentImage = this.car.media_urls.length - 1;
      }
    },
  },
  filters: {
    capitalise: function (input) {
      let capitalised = [];
      input.split(" ").forEach((word) => {
        capitalised.push(
          word.charAt(0).toUpperCase() + word.slice(1).toLowerCase()
        );
      });
      return capitalised.join(" ");
    },
  },
};
</script>

<style scoped lang="scss">
.card-container {
  border-radius: 1rem;
  box-shadow: 0 0 25px #00000022;
  overflow: hidden;

  .card-top {
    position: relative;

    .card-image {
      object-fit: cover;
      width: 100%;
      height: 250px;
    }

    .image-top {
      position: absolute;
      width: 100%;
      display: flex;
      justify-content: space-between;
      align-items: center;

      .classification {
        border-radius: 0.5rem;
        border: 1px solid #ffffff33;
        background: var(--dark1);
        color: white;
        padding: 0.25rem 0.5rem;
        margin: 0.625rem;
        font-size: 1rem;
      }

      .button-container {
        display: flex;
        align-items: center;
        margin-right: 0.625rem;

        p {
          color: white;
          margin-right: 0.3125rem;
        }

        button {
          border-radius: 0.5rem;
          background-color: var(--dark1);
          border: 1px solid #ffffff33;
          width: 2rem;
          height: 1.5rem;
          margin-left: 0.3125rem;

          img {
            width: 0.5rem;
            height: 0.5rem;
          }
        }
      }
    }

    .tags {
      position: absolute;
      bottom: 0;
      display: flex;

      p {
        border-radius: 0.5rem;
        border: 1px solid #ffffff33;
        background: var(--dark1);
        color: white;
        font-size: 0.75rem;
        padding: 0.0625rem 0.625rem;
        margin-left: 0.625rem;
        white-space: nowrap;
      }
    }
  }

  .card-bottom {
    padding: 0.625rem;

    .title-container {
      display: flex;
      align-items: flex-start;
      justify-content: space-between;

      .title-left {
        h3 {
          font-size: 1rem;
          font-weight: 400;
          margin-top: 0;
          margin-bottom: 0.3125rem;
          max-width: 98%;
        }

        p {
          margin: 0;
          font-weight: 300;
          font-size: 0.75rem;
          color: var(--grey1);
        }
      }

      img {
        cursor: pointer;
      }
    }

    .price {
      font-weight: 700;
      font-size: 20px;
      margin-top: 0.625rem;
      margin-bottom: 0.3125rem;

      span {
        font-size: 0.75rem;
        font-weight: 400;
      }
    }

    .price-when-new {
      margin: 0;
      font-size: 0.75rem;

      .calculate-link {
        color: var(--brand-primary);
        text-decoration: none;

        &:hover {
          text-decoration: underline;
        }
      }
    }
  }
}
</style>