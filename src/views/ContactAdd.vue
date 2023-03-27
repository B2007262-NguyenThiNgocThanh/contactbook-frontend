<script>

import ContactForm from "@/components/ContactForm.vue";
import ContactService from "@/services/contact.service";

export default {
    components: {
        ContactForm,
    },

    data() {
        return {
            contact: {
                name: "",
                email: "",
                address: "",
                phone: "",
                favorite: false
            },
            message: "",
        };
    },

    methods: {
        async addContact(data) {
            try {
                await ContactService.create(data);
                this.message = "Liên hệ được thêm mới thành công.";
            } catch (err) {
                console.log(err);
            }
        },
    },

    created() {
        this.message = "";
    },
};
</script>

<template>
    <div v-if="contact" class="page">
        <h4>Thêm Liên hệ</h4>
        <ContactForm 
            :contact="contact" 
            @submit:contact="addContact"
        />
        <p>{{ message }}</p>
    </div>
</template>