# Vue Image previewer

### Features & characteristics:

-   Showcase images that are not inside a vue component

### Example

## Install & basic usage
The component will create a gallery of a given image set.
When clicked on an image outside the component, the gallery will open at the given image.

```bash
npm install @salamander.be/vue-image-previewer
```

```vue
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
```

## Configuration

### Props

```js
images: ['/image-1.png', '/image-2.png'] // the items shown on the board
tergetClass: 'viewable-img' // The placeholder of the create option
```

### Events

```vue
<template>
    <kanban-board v-on:item-updated="handleItemUpdated" v-on:item-clicked="handleItemClicked" v-on:item-created="handleItemCreated"><kanban-board>
</template>

<script>
export default {
	methods: {
		handleItemUpdated(itemId, status, index) {
			// Update code
		},
		handleItemClicked(item) {
			// Clicked code
		},
		handleItemCreated(item) {
			// Created code
		}
	}
}
</script>
```
