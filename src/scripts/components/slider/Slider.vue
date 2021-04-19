<template lang="pug">
	.slider
		h1 Slider Apply
		.carousel__nav
			icon-button.carousel__nav__prev(
				label="Previous Slide",
				icon="arrow-left",
				@click="$refs.slider.slidePrev()"
			)
			icon-button.carousel__nav__next(
				label="Next Slide",
				icon="arrow-right",
				@click="$refs.slider.slideNext()"
			)
		carousel(
			ref="slider",
			:center-mode="centerMode",
			:infinite="infiniteScroll",
			:slides-to-show="slidesToShow",
			@before-slide="beforeSlide",
			@after-slide="afterSlide"
		)
			slide(v-for="(slide, index) in slides", :key="index + '_' + slide.id")
				slider-data(
					:title="slide.title",
					:description="slide.description",
					:headingcolor="slide.headingcolor",
					:subheadingcolor="slide.subheadingcolor",
					:btntextcolor="slide.btntextcolor",
					:btnbgcolor="slide.btnbgcolor",
					:headingfont="slide.headingfont",
					:headingweight="slide.headingweight",
					:subheadingfont="slide.subheadingfont",
					:subheadingweight="slide.subheadingweight",
					:buttonfont="slide.buttonfont",
					:buttonweight="slide.buttonweight",
					:btntext="slide.btntext",
					:btnlink="slide.btnlink",
					:image="slide.image",
					:textposition="slide.textposition",
					:mobile-image="slide.mobileImage",
					:sliderid="slide.id",
	    		)
</template>



<script>
  import Carousel from 'scripts/components/basic/Carousel.vue';
  import Slide from 'scripts/components/basic/Slide.vue';
  import SliderData from 'scripts/components/slider/SliderData.vue'; 
  import IconButton from 'scripts/components/buttons/IconButton.vue';

  export default {
    name: 'Slider',
    components: { Carousel, Slide, SliderData,IconButton },
    props: {
      title: String,
      slides: {
        type: Array,
        default: () => [],
      },
    },
    data() {
      return {
        activeIndex: null,
      };
    },
    computed: {
		slidesToShow() {
			console.log(this.slides);
			if (this.disableScroll) {
				return Math.min(this.slides.length, 1);
			}

			return this.$mq === 'mobile' ? 1.05 : 2;
		},
		disableScroll() {
			return Boolean(this.slides.length >= 1 && this.$mq !== 'mobile');
		},
		centerMode() {
			// not mobile and only 1 slide
			if (this.$mq !== 'mobile' && this.slides.length === 1) return true;

			// otherwise, set center mode when scroll is not disabled
			return !this.disableScroll;
		},
		infiniteScroll() {
			return !this.disableScroll;
		},
    },
    mounted() {
      this.activeIndex = 0;
    },
    methods: {
		beforeSlide({ from, to }) {
	        if (from !== to) this.activeIndex = null;
      	},	
      	afterSlide(index) {
	        this.activeIndex = index;
      	},
    },
  };
</script>

<style scoped lang="scss">
  .slider{
  	width:100%;
  }
  @media (max-width:1024px){
    .slider{
      height:100vh !important;
    }
  }
</style>