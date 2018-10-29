<template>
    <div id="app">
        <image-previewer :images="images" targetClass="viewable-img"></image-previewer>

        <!-- Content that is not inside the image-previewer component -->
        <div>
            <img style="width: 300px; height: 300px; object-fit: cover; margin: 15px;" v-for="(image, key) in images" :key="key" :src="image" class="viewable-img">
        </div>

    </div>
</template>

<script>
import ImagePreviewer from './components/image-previewer'

export default {
	name: 'app',
	components: {
		ImagePreviewer
	},
	data() {
		return {
			// Example: A list of random images
			images: [
                'https://picsum.photos/500/600', 
                'https://picsum.photos/700/500', 
                'https://picsum.photos/800/600', 
                'https://picsum.photos/800/700',
                'https://picsum.photos/900/500', 
                'https://picsum.photos/800/900', 
                'https://picsum.photos/700/900',
                'https://picsum.photos/500/900',
                ]
		}
	}
}
</script>
