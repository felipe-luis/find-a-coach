<template>
    <section>
        <CoachFilter @change-filter="setFilters">

        </CoachFilter>
    </section>
    <section>
        <BaseCard>
            <div class="controls">
                <BaseButton mode="outline">Refresh</BaseButton>
                <BaseButton v-if="!isCoach" link to="/register">Register as Coach</BaseButton>
            </div>
            <ul v-if="hasCoaches">
                <CoachItem v-for="coach in filteredCoaches" :key="coach" :id="coach.id" :firstName="coach.firstName"
                    :lastName="coach.lastName" :rate="coach.hourlyRate" :areas="coach.areas"></CoachItem>
            </ul>
            <h3 v-else>No coaches found.</h3>

        </BaseCard>
    </section>
</template>


<script>
import CoachFilter from '@/components/coaches/CoachFilter.vue';
import CoachItem from '@/components/coaches/CoachItem.vue';

export default {
    data(){
        return{
            activeFilters:{
                frontend: true,
                backend: true,
                career: true
            }
        }
    },
    components: {
        CoachItem,
        CoachFilter
    },
    computed: {
        filteredCoaches() {
            const coaches =  this.$store.getters['coaches/coaches'];
            return coaches.filter(coach => {
                if(this.activeFilters.frontend && coach.areas.includes('frontend')){
                    return true;
                }
                if(this.activeFilters.backend && coach.areas.includes('backend')){
                    return true;
                }
                if(this.activeFilters.career && coach.areas.includes('career')){
                    return true;
                }
                return false;
                
            })
        },
        hasCoaches() {
            return this.$store.getters['coaches/hasCoaches']
        },
        isCoach(){
            return this.$store.getters['coaches/isCoach']
        }
    }, 
    methods:{
        setFilters(updatedFilters){
            this.activeFilters = updatedFilters;
        }
    }
}

</script>

<style scoped>
ul {
    list-style: none;
    margin: 0;
    padding: 0;
}

.controls {
    display: flex;
    justify-content: space-between;
}
</style>