<template>
     <ul>
    <learning-resource v-for="item in resources" :key="item.id"
    :id="item.id"
    :title="item.title"
    :description="item.description"
    :link="item.link"
    ></learning-resource>
  </ul>
</template>
<script>
import LearningResource from './LearningResource';
export default {
    props: ['resources'],
    components: {
        LearningResource,
    }
}
</script>