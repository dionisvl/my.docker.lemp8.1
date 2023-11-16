<template>
    <div v-for="message in messages" class="chat-message">
        <div :class="{'justify-end': message.user.id != user.id}" class="flex items-end">
            <div :class="{'items-end': message.user.id != user.id, 'items-start': message.user.id == user.id}"
                 class="flex flex-col space-y-2 text-xs max-w-xs mx-2 order-2">
                <div>
                    <span :class="{'rounded-br-none bg-blue-600 text-white': message.user.id != user.id, 'rounded-bl-none bg-gray-300 text-gray-600': message.user.id == user.id}"
                          class="px-4 py-2 rounded-lg inline-block"
                    >
                        {{ message.message }}
                    </span>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import useChat from '../composables/chat';
import {onMounted} from 'vue';

export default {
    name: 'ChatMessages',
    props: {
        user: {
            required: true,
            type: Object
        }
    },
    setup() {
        const {messages, getMessages} = useChat()

        onMounted(getMessages)

        Echo.private('chat')
            .listen('MessageSent', (e) => {
                messages.value.push({
                    message: e.message.message,
                    user: e.user
                });
            });

        return {
            messages
        }
    }
};
</script>

<style scoped>

</style>
