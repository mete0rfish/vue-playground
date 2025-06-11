<template>
    <li>
        <h2>{{ name }} {{ isFavorate ? '(Favorate)' : '' }} </h2>
        <button @click="toggleIsFavorate">Favorate</button>
        <button @click="toggleDetails">Show Details</button>
        <ul v-if="detailsAreVisible">
            <li><strong>Phone: </strong> {{ phoneNumber }}</li>
            <li><strong>Email: </strong> {{ emailAddress }}</li>
        </ul>
        <button @click="$emit('delete', id)">Delete</button>
    </li>
</template>

<script>
export default {
    emits: ['toggle-favorate', 'delete'],
    // props: ['name', 'phoneNumber', 'emailAddress', 'isFavorate',],
    props: {
        id: {
            type: String,
            required: true,
        },
        name: {
            type: String,
            required: true,
        },
        phoneNumber: {
            type: String,
            required: true,
        },
        emailAddress: {
            type: String,
            required: true,
        },
        isFavorate: {
            type: Boolean,
            required: true,
            default: false,
        },
    },
    data() {
        return {
            detailsAreVisible: false,
        };
    },
    methods: {
        toggleDetails() {
            this.detailsAreVisible = !this.detailsAreVisible;
        },
        toggleIsFavorate() {
            this.$emit('toggle-favorate', this.id);
        },
    }
};
</script>