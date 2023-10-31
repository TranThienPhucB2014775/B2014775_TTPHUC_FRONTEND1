<template>
    <div v-if="contact" class="page">
        <h4>Thêm mới liên hệ</h4>
        <ContactFormAdd :contact="contact" @submit:contact="addContact" />
        <p>{{ message }}</p>
    </div>
</template>
<script>
import ContactService from "@/services/contact.service";
import ContactFormAdd from "./ContactFormAdd.vue";
export default {
    components: {
    ContactFormAdd
},
    data() {
        return {
            contact: this.contact,
            message: "",
        };
    },
    
    methods: {
        // async getContact(id) {
        //     this.contact = null   
        // },
        async addContact(data) {
            try {
                // console.log(data);
                await ContactService.add(data);
                this.message = "Liên hệ được thêm mới thành công.";
            } catch (error) {
                console.log(error);
            }
        },
    },
    created() {
        this.contact = {}
        this.message = "";
    },
};
</script>