<template>
    <base-card>
        <base-button @click="setSelectedTap('stored-resources')" :mode="storedResButtonMode">Stored Resources</base-button>
        <base-button @click="setSelectedTap('add-resource')" :mode="addResButtonMode">Add Resource</base-button>
    </base-card>
    <KeepAlive>
        <component :is="selectedTap"></component>
    </KeepAlive>   
</template>

<script>
import AddResource from './AddResource.vue';
import StoredResources from './StoredResources.vue'

export default {
    components: {
        StoredResources,
        AddResource,
    },
    data() {
        return {
            selectedTap: 'stored-resources',
            storedResources: [
                { 
                    id: 'official-guide', 
                    title: 'official Guide', 
                    description: 'The official Vue.js Documentation',
                    link: 'https://vuejs.org'
                },
                { 
                    id: 'google', 
                    title: 'Google', 
                    description: 'Learn to google...',
                    link: 'https://google.com'
                },
            ],
        };
    },
    provide() {
        return {
            resources: this.storedResources,
            addResource: this.addResource,
            deleteResource: this.removeResource,
        }
    },
    computed: {
        storedResButtonMode() {
            return this.selectedTap === 'stored-resources' ? null : 'flat';
        },
        addResButtonMode() {
            return this.selectedTap === 'add-resource' ? null : 'flat';
        }
    },
    methods: {
        setSelectedTap(tap) {
            this.selectedTap = tap;
        },
        addResource(title, description, link) {
            const newResource = {
                id: new Date().toISOString(),
                title: title,
                description: description,
                link: link
            };
            this.storedResources.unshift(newResource);
            this.selectedTap = 'stored-resources';
        },
        removeResource(resId) {
            const resIndex = this.storedResources.findIndex(res => res.id === resId);
            this.storedResources.splice(resIndex, 1);
        },
    }
}
</script>