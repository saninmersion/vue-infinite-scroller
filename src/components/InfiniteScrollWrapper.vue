<template>
    <div ref="wrapper" class="wrapper">
        <slot/>
        <div ref="end" class="scroll_end">
            <span v-if="showMore">Load More</span>
        </div>
    </div>
</template>

<script>
    import { onMounted, ref } from "vue"
    export default {
        name: "InfiniteScrollWrapper",

        props: {
            showMore: { type: Boolean, default: true },
            threshold: { type: Number, default: 0 },
        },

        setup(props, { emit }) {
            const wrapper = ref(null)
            const end = ref(null)

            onMounted(() => {
                const observer = new IntersectionObserver((entries) => {
                    entries.forEach(entry => {
                        if (entry.isIntersecting) {
                            emit("infinite")
                        }
                    })
                }, { root: wrapper.value, threshold: props.threshold })

                observer.observe(end.value)
            })

            return {
                end,
                wrapper,
            }
        },
    }
</script>

<style lang="css">
    .wrapper {
        border: 2px;
        height: 500px;
        overflow: auto;
    }

    .scroll_end span {
        height: 50px;
        margin: 0 auto;
        display: flex;
        justify-content: center;
        background: gray;
        align-items: center;
        color: white;
    }
</style>