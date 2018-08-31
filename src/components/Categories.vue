<template>
    <Page class="page" backgroundSpanUnderStatusBar="true">

        <ActionBar flat="true" class="action-bar" title="">
            <NavigationButton text="" android.systemIcon="ic_menu_back" />
        </ActionBar>

        <StackLayout v-if="categories.length < 0" v-for="category in categories">
            <Label :text="category"></Label>
        </StackLayout>
    </Page>
</template>

<script>
    import Settings from '../Settings';

    export default {

        data() {
            return {
                categories: []
            }
        },

        created() {
            this.getCategories();
        },
        methods: {
            getCategories() {
                fetch(`${Settings.BASE_URL}/jokes/categories`, {
                    method: 'GET'
                }).then((result) => {
                    return result.json();
                }).then((response) => {
                    this.categories = response;
                    console.log('Test:', response);
                }).catch((error) => {
                    console.log(error);
                });
            }
        }
    }
</script>