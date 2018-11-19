<style lang="scss" scoped>
.preview-backdrop {
	position: fixed;
	height: 100vh;
	width: 100vw;
	cursor: pointer;
	background-color: rgba(75, 83, 95, 0.8);
	top: 0;
	left: 0;
	z-index: 10000;
	.preview-container {
		height: 100%;
		width: 100%;
		padding-right: 15px;
		padding-left: 15px;
		margin-right: auto;
		margin-left: auto;
		@media (min-width: 576px) {
			max-width: 540px;
		}
		@media (min-width: 768px) {
			max-width: 720px;
		}
		@media (min-width: 992px) {
			max-width: 960px;
		}
		@media (min-width: 1200px) {
			max-width: 1200px;
		}
		.preview-row {
			height: 100%;
			display: flex;
			flex-wrap: wrap;
			margin-right: -15px;
			margin-left: -15px;
			.preview-content {
				position: relative;
				width: 100%;
				min-height: 1px;
				padding-right: 15px;
				padding-left: 15px;
				flex: 0 0 100%;
				margin: auto;

				img {
					object-fit: cover;
					cursor: default;
					user-select: none;
					max-height: 80vh;
					object-fit: contain;
					height: 100%;
					width: 100%;
				}
			}
		}
	}

	.close {
		color: #fff;
		position: absolute;
		top: 30px;
		right: 30px;
		cursor: pointer;
		transition: color 0.3s;
		&:hover {
			color: #565656;
		}
		svg {
			width: 20px;
		}
	}
	.arrow {
		user-select: none;
		color: #fff;
		position: absolute;
		top: 0;
		bottom: 0;
		margin: auto;
		height: 50px;
		cursor: pointer;
		width: 50px;
		padding: 15px;
		transition: color 0.3s;
		&:hover {
			color: #565656;
		}
		&.prev {
			left: -25px;
		}
		&.next {
			right: -25px;
		}
		svg {
			width: 20px;
		}
	}
}
</style>

<style>
*,
*::before,
*::after {
	-webkit-box-sizing: border-box;
	box-sizing: border-box;
}
.viewable-img {
	cursor: pointer;
}
</style>

<template>
    <div class="preview-backdrop" v-if="open" @click="close">
        <span v-show="index !== 0" class="prev arrow"  @click.stop="prev()">
            <svg data-v-7008925b="" class="svg-inline--fa fa-long-arrow-left fa-w-14" aria-hidden="true" data-prefix="fal" data-icon="long-arrow-left" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" data-fa-i2svg="">
                <path fill="currentColor" d="M136.97 380.485l7.071-7.07c4.686-4.686 4.686-12.284 0-16.971L60.113 273H436c6.627 0 12-5.373 12-12v-10c0-6.627-5.373-12-12-12H60.113l83.928-83.444c4.686-4.686 4.686-12.284 0-16.971l-7.071-7.07c-4.686-4.686-12.284-4.686-16.97 0l-116.485 116c-4.686 4.686-4.686 12.284 0 16.971l116.485 116c4.686 4.686 12.284 4.686 16.97-.001z"></path>
            </svg>
        </span>
        <div class="preview-container">
            <div class="preview-row">
                <span class="close" @click="close">
                    <svg data-v-7008925b="" class="svg-inline--fa fa-times fa-w-12" aria-hidden="true" data-prefix="fal" data-icon="times" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 384 512" data-fa-i2svg="">
                        <path fill="currentColor" d="M217.5 256l137.2-137.2c4.7-4.7 4.7-12.3 0-17l-8.5-8.5c-4.7-4.7-12.3-4.7-17 0L192 230.5 54.8 93.4c-4.7-4.7-12.3-4.7-17 0l-8.5 8.5c-4.7 4.7-4.7 12.3 0 17L166.5 256 29.4 393.2c-4.7 4.7-4.7 12.3 0 17l8.5 8.5c4.7 4.7 12.3 4.7 17 0L192 281.5l137.2 137.2c4.7 4.7 12.3 4.7 17 0l8.5-8.5c4.7-4.7 4.7-12.3 0-17L217.5 256z"></path>
                    </svg>
                </span>
                <div @click.stop class="preview-content">
                    <img class="main-img" :src="viewing">
                </div>
            </div>
        </div>
        <span v-show="index !== images.length - 1" class="next arrow" @click.stop="next()">
            <svg data-v-7008925b="" class="svg-inline--fa fa-long-arrow-right fa-w-14" aria-hidden="true" data-prefix="fal" data-icon="long-arrow-right" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" data-fa-i2svg="">
                <path fill="currentColor" d="M311.03 131.515l-7.071 7.07c-4.686 4.686-4.686 12.284 0 16.971L387.887 239H12c-6.627 0-12 5.373-12 12v10c0 6.627 5.373 12 12 12h375.887l-83.928 83.444c-4.686 4.686-4.686 12.284 0 16.971l7.071 7.07c4.686 4.686 12.284 4.686 16.97 0l116.485-116c4.686-4.686 4.686-12.284 0-16.971L328 131.515c-4.686-4.687-12.284-4.687-16.97 0z"></path>
            </svg>
        </span>
    </div>
</template>

<script>
export default {
	props: {
		/**
		 * Array that lists all the available images
		 * @default '[]'
		 * @type {Array}
		 */
		images: {
			default: () => {
				return []
			}
		},
		/**
		 * String that defines the target class
		 * @default 'viewable-img'
		 * @type {String}
		 */
		targetClass: {
			default: 'viewable-img'
		}
	},
	data() {
		return {
			open: false,
			viewing: '',
			index: false
		}
	},
	created() {
		let self = this

		// Add a listener to check when an image with the
		// target class hass been clicked.
		document.addEventListener('click', function(event) {
			if (self.hasClass(event.target, self.targetClass)) {
				self.open = true
				if (event.target.nodeName.toLowerCase() === 'img') {
					self.viewing = event.target.src
				} else {
					self.viewing = event.target.getAttribute('data-url')
				}
				self.index = self.images.indexOf(self.viewing)
				document.querySelector('body').style.overflow = 'hidden'
				document.querySelector('html').style.overflow = 'hidden'
				self.setArrows()
			}
		})
		window.addEventListener('keyup', function(event) {
			if (event.keyCode == 37) {
				self.prev()
			}
			if (event.keyCode == 39) {
				self.next()
			}
		})
	},
	methods: {
		close() {
			this.viewing = ''
			this.open = false
			this.index = false
			document.querySelector('body,html').style.overflow = 'auto'
			document.querySelector('html').style.overflow = 'auto'
		},
		prev() {
			if (this.index !== 0) {
				this.viewing = this.images[this.index - 1]
				this.index--
				this.setArrows()
			}
		},
		next() {
			if (this.index !== this.images.length - 1) {
				this.viewing = this.images[this.index + 1]
				this.index++
				this.setArrows()
			}
		},
		setArrows() {
			this.$nextTick(function() {
				document.querySelector('.arrow.prev').style.left = '+' + document.querySelector('.main-img').offsetLeft / 2 + 'px'
				document.querySelector('.arrow.next').style.right = '+' + document.querySelector('.main-img').offsetLeft / 2 + 'px'
			})
		},
		/*
        * Check if a given element has a specific class
        * Returns Boolean
        */
		hasClass(target, className) {
			return new RegExp('(\\s|^)' + className + '(\\s|$)').test(target.className)
		}
	}
}
</script>
