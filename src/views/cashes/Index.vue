<template>
    <div class="container mx-auto">
        <div class="w-full lg:w-8/12">
            <div class="w-full mb-8">
                <div class="bg-gray-200 rounded-2xl -rotate-2 transform">
                    <div
                        class="
                            bg-gradient-to-br
                            from-blue-500
                            to-light-blue-400
                            text-white
                            rounded-2xl
                            rotate-2
                            transform
                            p-5
                        "
                    >
                        <label
                            class="
                                block
                                uppercase
                                font-semibold
                                text-xs text-blue-50
                                tracking-wider
                                mb-2
                            "
                            >Balances</label
                        >
                        <div class="text-3xl font-semibold">
                            Rp. {{ state.balances }}
                        </div>
                    </div>
                </div>
            </div>
            <div class="flex items-center -mx-2">
                <div class="w-full px-2">
                    <div class="bg-gray-200 rounded-2xl -rotate-3 transform">
                        <div
                            class="
                                bg-gradient-to-br
                                from-teal-500
                                to-cyan-400
                                text-white
                                rounded-2xl
                                rotate-3
                                transform
                                p-5
                            "
                        >
                            <label
                                class="
                                    block
                                    uppercase
                                    font-semibold
                                    text-xs text-blue-50
                                    tracking-wider
                                    mb-2
                                "
                                >Debit</label
                            >
                            <div class="text-3xl font-semibold">
                                Rp. {{ state.debit }}
                            </div>
                        </div>
                    </div>
                </div>
                <div class="w-full px-2">
                    <div class="bg-gray-200 rounded-2xl -rotate-3 transform">
                        <div
                            class="
                                bg-gradient-to-br
                                from-red-500
                                to-yellow-400
                                text-white
                                rounded-2xl
                                rotate-3
                                transform
                                p-5
                            "
                        >
                            <label
                                class="
                                    block
                                    uppercase
                                    font-semibold
                                    text-xs text-blue-50
                                    tracking-wider
                                    mb-2
                                "
                                >Credit</label
                            >
                            <div class="text-3xl font-semibold">
                                Rp. {{ state.credit }}
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <div class="my-10 border rounded-lg overflow-hidden h-">
                <div class="border-b px-6 py-4 bg-gray-50">Transaction</div>
                <div class="h-112 overflow-y-scroll">
                    <template
                        v-for="transaction in state.transactions"
                        :key="transaction.id"
                    >
                        <a
                            href=""
                            class="
                                border-b
                                px-6
                                py-4
                                flex
                                justify-between
                                items-center
                                hover:bg-gray-50
                            "
                        >
                            <span class="flex flex-col">
                                <span class="text-gray-500 text-xs">{{
                                    transaction.when
                                }}</span>
                                <span>{{ transaction.name }}</span>
                            </span>
                            <span
                                :class="
                                    transaction.isCredit
                                        ? 'text-green-500'
                                        : 'text-red-500'
                                "
                                >Rp. {{ transaction.amount }}</span
                            >
                        </a>
                    </template>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import { onMounted, ref } from "vue";
import axios from "axios";
export default {
    setup() {
        const state = ref([]);

        const getCashes = async () => {
            let { data } = await axios.get("api/cash");
            state.value = data;
        };

        onMounted(() => {
            getCashes();
        });

        return { state };
    },
};
</script>

<style>
</style>