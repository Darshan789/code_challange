<template lang="pug">
  .slider-data
    .slider-data__main_content
        img(v-if="$mq === 'mobile'", :src="mobileImage")
        img(v-else, :src="image")
    transition(name="fade-slow")
      .slider_text_wrapper.text_cover(:class="textposition")
        .slider-data__title.heading(:class="'heading_'+sliderid", :style="{color: headingcolor, fontFamily: headingfont, fontWeight: headingweight}") {{ title }}
        .slider-data__description.subheading(:class="'subheading_'+sliderid", :style="{color: subheadingcolor, fontFamily: subheadingfont, fontWeight: subheadingweight}") {{ description }}
        a.btn(:href="btnlink", :class="'button_'+sliderid", :style="{color: btntextcolor, fontFamily: headingfont, fontWeight: headingweight, backgroundColor: btnbgcolor}") {{ btntext }}
</template>

<script>

export default {
    name: 'SliderData',
    props: {
      title: String,
      image: String,
      mobileImage: String,
      description: String,
      btntext: String,  
      btnlink: String,
      sliderid: String,
      textposition: String,
      headingcolor: String,
      subheadingcolor: String,
      btntextcolor: String,
      btnbgcolor: String,
      headingfont: String,
      headingweight: String,
      subheadingfont: String,
      subheadingweight: String,
      buttonfont: String,
      buttonweight: String
    },
    computed: {

    },
    methods: {
    },
  };
</script>

<style lang="scss">
  .slider-data{
    position:relative;
  }
  .text_cover {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    max-width: 56%;
  }
  .text_cover.left{
    left:78px;
  }
  .text_cover.right{
    left:auto;
    right:78px;
    max-width: 45%;
  }
  .text_cover.center{
    left:50%;
    transform: translate(-50%,-50%);
    text-align:center;
  }
  .text_cover.center .subheading{
    margin:0 auto 45px;
    max-width: 100%;
  }
  .subheading{
    max-width: 75%;
    font-size:24px;
    margin-bottom:45px;
  }
  .text_cover.right .subheading{
    max-width:100%;
  }
  .heading{
    font-size:46px;
    margin-bottom:5px;
    text-transform:none;
    letter-spacing:normal;
  }
  .btn{
    font-size:20px;
    border-radius:25px;
    line-height:34px;
    width:213px;
    display:inline-block;
    text-align: center;
    padding: 10px 0;
  }
  @media (max-width:1024px){
    .text_cover{
      max-width: 90% !important;
      text-align: center;
      margin: 0 auto;
      left: 50% !important;
      transform: translate(-50%,-50%);
      width: 90%;
      right: 0 !important;
    }
    .text_cover.left .subheading{
      margin:0 auto 45px;
      max-width: 100%;
    }
  }
</style>