<template>
  <div class="category-book-main">
    <title-view
      :label="categoryText(data.category)"
      :btn="$t('home.seeAll')"
      @onClick="showBookCategory"
    ></title-view>
    <div class="category-book-list">
      <div
        class="category-book-item"
        v-for="(item, index) in data.list"
        :key="index"
        @click="showBookDetail(item)"
      >
        <div class="img-wrapper">
          <img class="img" v-lazy="item.cover" />
        </div>
        <div class="content-wrapper">
          <div class="title title-small" ref="title">{{item.title}}</div>
          <div class="num sub-title-tiny" ref="author">{{item.author}}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import TitleView from "@/components/home/title";
import { categoryText, getCategoryName } from "@/utils/home";
import { StoreHomeMixin } from "@/mixins/home";

export default {
  name:"CategoryBook",
  mixins: [StoreHomeMixin],
  components: {
    TitleView
  },
  props: {
    data: Object
  },
  methods: {
    showBookCategory() {
      this.$router.push({
        name: "bookList",
        query: {
          category: getCategoryName(this.data.category),
          categoryText: this.categoryText(this.data.category)
        }
      });
    },
    
    categoryText(category) {
      return categoryText(category, this);
    }
  }
};
</script>

<style lang="scss" scoped>
.category-book-main {
  .category-book-list {
    width: 100%;
    @include top;
    padding: 0 5px;
    box-sizing: border-box;
    .category-book-item {
      flex: 0 0 25%;
      width: 25%;
      padding: 0 5px;
      box-sizing: border-box;
      .img-wrapper {
        @include center;
        .img {
          width: 100%;
        }
      }
      .content-wrapper {
        width: 100%;
        margin-top: 10px;
        .num {
          margin-top: 5px;
        }
      }
    }
  }
}
</style>
