<template>
    <div class="page">
        <h4>Thêm liên hệ</h4>
        <ContactForm :contact="contact" @submit:contact="addContact" />
    </div>
</template>

<script>
import ContactForm from '@/components/ContactForm.vue';
import ContactService from '@/services/contact.service';

export default {
    components: {
        ContactForm,
    },
    data() {
        return {
            contact: {
                name: '',
                email: '',
                address: '',
                phone: '',
                favorite: false,
            },
            message: '',
        };
    },
    methods: {
        async addContact(data) {
            try {
                await ContactService.create(data);
                alert("Liên hệ được thêm thành công");   //tao thông báo đã thêm thành công
                this.$router.push({ name: 'contactbook' });
            } catch (err) {
                console.log(err);
            }
        },
    },
    created() {
        this.message = '';
    },
};
</script>