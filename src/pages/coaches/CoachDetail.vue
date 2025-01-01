<template>
    <section>
        <BaseCard>
            <h2>{{ fullName }}</h2>
            <h3>${{ rate }}/hour</h3>
        </BaseCard>
    </section>

    <section>
        <BaseCard>
            <header>
                <h2>Interested? Reach out now!</h2>
                <BaseButton link :to="contactLink">Contact</BaseButton>
            </header>
            <RouterView></RouterView>
        </BaseCard>
    </section>

    <section>
        <BaseCard>
            <BaseBadge v-for="area in areas" :key="area" :type="area" :title="area"> {{ area }}</BaseBadge>
            <p>{{ description }}</p>
        </BaseCard>
    </section>
</template>

<script>

export default{
    props:['id'],
    data(){
        return {
            selectedCoach: null,
        }
    },

    created(){
        this.selectedCoach = this.$store.getters['coaches/coaches'].find(coach => coach.id === this.id);
    },
    computed:{
        contactLink(){
            return this.$route.path + '/contact';
        },
        fullName(){
            return this.selectedCoach.firstName + ' ' + this.selectedCoach.lastName;
        },
        rate(){
            return this.selectedCoach.hourlyRate;
        },
        areas(){
            return this.selectedCoach.areas;
        },
        description(){
            return this.selectedCoach.description;
        }
    }
}
</script>