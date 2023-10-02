<template>
  <div id="kakao_map" style="width: 100%; height: 100vh"></div>
</template>

<script>
const kakao = window.kakao;

export default {
  name: "KakaoMap",
  mounted() {
    this.initMap();
  },
  methods: {
    initMap() {
      var container = document.getElementById("kakao_map"); //지도를 담을 영역의 DOM 레퍼런스
      var options = {
        //지도를 생성할 때 필요한 기본 옵션
        center: new kakao.maps.LatLng(33.450701, 126.570667), //지도의 중심좌표.
        level: 3, //지도의 레벨(확대, 축소 정도)
      };

      new kakao.maps.Map(container, options); //지도 생성 및 객체 리턴
    },
  },
};
</script>

<style></style>
