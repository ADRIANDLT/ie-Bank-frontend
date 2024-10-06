<template>
    <div>
        <h1>Skull</h1>
       
        <h3>FrontEnd Skull's info</h3>
        <p>Environment: {{ environment }}</p>
        <p>Environment Variable File Name: {{ env_var_file_name }}</p>
        <p>REST API uri: {{ rest_api_uri }}</p>
 
        <h3>BackEnd Skull's info</h3>
        <p>{{ msg }}</p>
    </div>
</template>
 
<script>
import axios from 'axios'
export default
    {
        name: 'Skull',
        data() {
            return {
                msg: `Hi! This is the skull component 💀, running in mode: ${process.env.NODE_ENV} with environment variables defined in ${process.env.VUE_APP_ENV_VAR_FILE_NAME}`,
                environment: '',
                rest_api_uri: '',
                env_var_file_name: ''
            }
        },
        methods:
        {
            getSkull() {
                const path = `${process.env.VUE_APP_ROOT_URL}/skull`;
                axios.get(path)
                    .then((response) => {
                        this.msg = response.data;
                    })
                    .catch(error => console.log(error))
            }
        },
        created() {
            this.environment = process.env.NODE_ENV;
            this.rest_api_uri = process.env.VUE_APP_ROOT_URL;
            this.env_var_file_name = process.env.VUE_APP_ENV_VAR_FILE_NAME;
 
            this.getSkull()
        }
 
 
    }
</script>