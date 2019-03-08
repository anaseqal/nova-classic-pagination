<template>
    <div class="bg-20 rounded-b">
        <nav class="inline-flex items-center p-3">

            <!-- First Link -->
            <button
                :disabled="!hasPreviousPages"
                class="bg-transparent border border-primary text-primary font-bold py-2 px-4 rounded-l border-r-0"
                :class="{
                    'dim': hasPreviousPages,
                    'opacity-50': !hasPreviousPages,
                }"
                rel="prev"
                @click.prevent="selectFirstPage()"
                dusk="previous"
            >
                {{ __('First') }}
            </button>

            <!-- Previous Link -->
            <button
                v-if="hasPreviousPages"
                :disabled="!hasPreviousPages"
                class="bg-transparent border border-primary text-primary font-bold py-2 px-4"
                :class="{
                    'dim': hasPreviousPages,
                    'opacity-50': !hasPreviousPages,
                }"
                rel="prev"
                @click.prevent="selectPreviousPage()"
                dusk="previous"
            >
                {{ this.page-1 }}
            </button>

            <!-- Current Page -->
            <button
                disabled="disabled"
                class="bg-primary border border-primary text-white font-bold py-2 px-4"
                rel="current"
                dusk="current"
            >
                {{ this.page }}
            </button>

            <!-- Next Link -->
            <button
                v-if="hasMorePages"
                :disabled="!hasMorePages"
                class="bg-transparent border border-primary text-primary font-bold py-2 px-4"
                :class="{
                    'dim': hasMorePages,
                    'opacity-50': !hasMorePages,
                }"
                rel="next"
                @click.prevent="selectNextPage()"
                dusk="next"
            >
                {{ this.page+1 }}
            </button>

            <!-- Last Link -->
            <button
                :disabled="!hasMorePages"
                class="bg-transparent border border-primary text-primary font-bold py-2 px-4 rounded-r border-l-0"
                :class="{
                    'dim': hasMorePages,
                    'opacity-50': !hasMorePages,
                }"
                rel="next"
                @click.prevent="selectLastPage()"
                dusk="next"
            >
                {{ __('Last') }}
            </button>

            <slot />

        </nav>
    </div>
</template>

<script>
export default {
    props: {
        page: {
            type: Number,
            required: true,
        },
        pages: {
            type: Number,
            default: 0,
        },
        next: {
            type: Boolean,
            default: false,
        },
        previous: {
            type: Boolean,
            default: false,
        },
    },

    methods: {
        /**
         * Select first page.
         */
        selectFirstPage() {
            this.selectPage(1)
        },

        /**
         * Select last page.
         */
        selectLastPage() {
            this.selectPage(this.pages)
        },

        /**
         * Select the previous page.
         */
        selectPreviousPage() {
            this.selectPage(this.page - 1)
        },

        /**
         * Select the next page.
         */
        selectNextPage() {
            this.selectPage(this.page + 1)
        },

        /**
         * Select the page.
         */
        selectPage(page) {
            this.$emit('page', page)
        },
    },

    computed: {
        /**
         * Determine if prior pages are available.
         */
        hasPreviousPages: function() {
            return this.previous
        },

        /**
         * Determine if more pages are available.
         */
        hasMorePages: function() {
            return this.next
        },
    },
}
</script>
