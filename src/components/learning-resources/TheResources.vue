<template>
    <base-card>
        <base-button @click="setSelectedTab('stored-resources')" 
        :mode="storedResourceButtonMode">Stored Resources</base-button>
        <base-button @click="setSelectedTab('add-resource')"
        :mode="addResourceButtonMode"
        >Add Resource</base-button>
    </base-card>
    <keep-alive>
         <component :is="selectedTab"></component>
    </keep-alive>
   
</template>
<script>
import StoredResources from './StoredResources';
import AddResource from './AddResource';
export default {
    components: {
        StoredResources,
        AddResource,
    },
    data () {
        return {
            selectedTab: 'stored-resources',
            storedResources: [
                {   
                    id: 'official-guide',
                    title: 'Official Guide',
                    description: 'The official Vue.js Documentation',
                    link: 'https://vuejs.org',
                },
                {
                    id: 'google',
                    title: 'Google',
                    description: 'Learn to google... ',
                    link: 'https://google.ie',
                }
            ]   
        }
    },
    provide () {
        return {
            resources: this.storedResources,
            addResource: this.addResource,
            deleteResource: this.removeResource,
        }
    },
    methods: {
        setSelectedTab(tab) {
            this.selectedTab = tab
        },
        addResource(title, description, url) {
            const newResource = {
                id: new Date().toISOString(),
                title: title,
                description: description,
                link: url,
            }
            this.storedResources.unshift(newResource);
            this.selectedTab = 'stored-resources';
        },
        removeResource(id) {
           const resourceIndex = this.storedResources.findIndex(function (res) {
               return res.id === id;
           }) 
           this.storedResources.splice(resourceIndex, 1);
        },
    },
    computed: {
        storedResourceButtonMode() {
            return this.selectedTab === 'stored-resources' ? null : 'flat';
        },
        addResourceButtonMode() {
            return this.selectedTab === 'add-resource' ? null : 'flat';
        }
    },
}
</script>