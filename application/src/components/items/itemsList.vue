<template>

</template>

<script>
import testData from "../../utilities/testData.js";
export default {
  data() {
    return {
      itemsList: [],
      msg: ""
    };
  },
  methods: {
    getImgUrl(img) {
      return img ? require(`../../assets/${img}`) : "";
    },
    goto(id) {
      return `/category/${id}`;
    },
    getCategoryDescription(id){
        
    }
  },
  mounted() {
    let parentsId = this.$route.params.categoryId;
    this.itemsList = testData.items.filter(function(i) {
      return filtredArr(i.parentId);
    });
    function filtredArr(id) {
      return id === parentsId;
    }
    console.log(this.itemsList, 2);
  }
};
</script>

<style scoped>
.items-wrap {
  /* border: 1px solid #017493; */
}
.description {
  text-align: center;
}
.btn-primary,
.btn-primary:not(:disabled):not(.disabled):active {
  color: #017493;
  border-color: #017493;
  background: white;
  border-radius: 0rem;
  font-weight: 600;
}
.card-text {
  color: #017493;
  font-weight: 600;
}
.btn-primary:focus,
.btn-primary:not(:disabled):not(.disabled):active:focus {
  box-shadow: none;
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 2s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active до версии 2.1.8 */ {
  opacity: 0;
}
span {
  display: contents;
}
</style>


