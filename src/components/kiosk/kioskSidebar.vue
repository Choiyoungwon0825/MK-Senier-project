<template>
  <v-app-bar app>
    <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
  </v-app-bar>

  <v-navigation-drawer v-model="drawer" app>
    <!-- 여기에 사이드 바 내용을 넣습니다. -->
    <v-list>
      <!--marker에게 전달 받은 내용이 있으면 표시-->
      <v-list-item v-if="marker">
        <v-list-item-content>
          <v-list-item-title>
            <div class="name">
              상점이름 : 
              <span>{{ marker.storeName }}</span>
            </div>
          </v-list-item-title>
          
          <v-img :src="marker.image" />

          <div v-if="marker.reviews.length === 0" class="sidestyle">
            <div class="review">등록 후기</div>
            <v-list-item-subtitle>리뷰가 없습니다.</v-list-item-subtitle>
          </div>
          <div v-for="(review, index) in marker.reviews" :key="index">
            <v-list-item-subtitle>이름 : {{ review.name }}</v-list-item-subtitle>
            <v-list-item-subtitle>별점 : {{ review.rating }}</v-list-item-subtitle>
            <v-list-item-subtitle>리뷰내용 : {{ review.comment }}</v-list-item-subtitle>
          </div>

          <!-- 여기에 필요한 정보를 추가하세요 -->
        </v-list-item-content>
      </v-list-item>
    </v-list>
  </v-navigation-drawer>
</template>

<script>
export default {
  name: 'kioskSidebar',
  props: {
    marker: Object,
    drawerOpen: Boolean,
  },
  data() {
    return {
      drawer: this.drawerOpen,
    };
  },
  watch: {
    // drawerOpen prop의 값이 변경될 때마다 drawer의 값도 변경
    drawerOpen(newVal) {
      this.drawer = newVal;
    },
    // drawer의 값이 변경될 때마다 update:drawerOpen 이벤트 발생
    drawer(newVal) {
      this.$emit('update:drawerOpen', newVal);
    },
  },
};
</script>

<style>
.name{
  text-align: center;
  font-weight: bold;
  border: 1px solid #444444;
  margin-bottom: 12px;
}
.review{
  margin-top: 12px;
  color: #444444;

}
.sidestyle{
  text-align: center;
}
</style>