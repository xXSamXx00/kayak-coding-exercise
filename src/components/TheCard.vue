<template>
  <div class="col">
    <div class="card">
      <div class="card-img">
        <img height="50" :src="'https://www.kayak.com' + img" :alt="name" />
      </div>
      <div class="info">
        <p class="company-title">{{ name }}</p>
        <p class="company-alliance" v-if="alliance !== 'none'">
          {{ alliances[alliance] }}
        </p>
        <p class="company-phone" v-if="phone !== ''">
          {{ phone }}
        </p>
        <p class="company-website" v-if="website !== ''">
          <a :href="website">{{ shortLink }}</a>
        </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      alliances: {
        ST: "Sky Team",
        OW: "Oneworld",
        SA: "Star Alliance",
      },
      shortLink: null,
    };
  },
  props: {
    name: String,
    img: String,
    alliance: String,
    phone: String,
    website: String,
  },
  mounted() {
    let link = this.website;
    if (link.startsWith("http")) {
      link = link.substr(8);
    }
    if (link.startsWith("www")) {
      link = link.substr(4);
    }
    if (link.includes("/")) {
      let i = link.indexOf("/");
      link = link.substring(0, i);
    }
    this.shortLink = link;
  },
};
</script>

<style lang="scss">
.col {
  margin-top: 16px;
  .card {
    background-color: white;
    box-shadow: 0 -1px 4px 0 rgba(25, 32, 36, 0.04),
      0 3px 6px 0 rgba(25, 32, 36, 0.16);
    border-radius: 8px;
    width: 300px;
    height: 240px;
    display: flex;
    align-items: center;
    &:hover {
      border: 1px solid #363f45;
      .info {
        .company-alliance,
        .company-phone,
        .company-website {
          display: block;
        }
      }
    }
    .card-img {
      width: 100px;
      display: flex;
      justify-content: flex-end;
      img {
        width: 32px;
        height: 32px;
        margin-right: 18px;
      }
    }
    .info {
      .company-title {
        font-size: 16px;
        font-weight: bold;
      }
      .company-alliance {
        color: #192024;
      }
      .company-phone,
      .company-website a {
        color: #5a6872;
        text-decoration: none;
      }
      .company-alliance,
      .company-phone,
      .company-website {
        display: none;
        font-size: 14px;
      }
    }
  }
}
</style>
