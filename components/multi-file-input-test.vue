Wrapper for multi-file input.

<template>
    <form @submit.prevent="submit">
        <input type="text" v-model="form.text">
        <input type="file" v-el:many-files multiple>
        <pre v-text="$data | json"></pre>

        <button type="submit">Отправить</button>
    </form>
</template>

<script>
    import $ from 'jquery'

    export default {

        data: function () {
            return {
                form: {
                    text: '',
                }
            }
        },
        methods: {

            submit: function () {
                var files = this.$els.manyFiles.files
                var data = new FormData

                for(var key in files){
                    data.append('files['+key+']', files[key]);
                }

                $.ajax({
                    url: '/test',
                    type: 'POST',
                    data,
                    cache: false,
                    contentType: false,
                    processData: false
                })
            }
        },
    }
</script>