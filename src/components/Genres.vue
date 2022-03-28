<template>
  <div>
    <div class="genresBtn">
      #{{genres}}
    </div>
  </div>
</template>

<script>
export default {
  name: 'Generes',
  props: {
    genres: String
  }
}
</script>

<style>
.genresBtn{
  color: #fff;
  font-size: 18px;
  background-color: #a734ff;
  width: 100px;
  height: 30px;
  text-align: center;
  border-radius: 15px;
  line-height: 30px;
  margin-right: 20px;
  margin-bottom: 10px;
}
</style>