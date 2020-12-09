<template>
    <div class="paginated-content">
        <div class="container">
            <div class="row breadcrumbs justify-content-center mb-2">
                <div class="col-lg-8 col-md-10 col-sm-12">
                    <nav>
                        <ol class="breadcrumb justify-content-between">
                            <li class="breadcrumb-item no-icon"
                                v-for="(step, index) in steps" :key="index"
                                v-bind:class="{ active: stepIsActive(index) }">
                                <a v-on:click="setStepIfAllowed(index)">{{ step.title }}</a>
                            </li>
                        </ol>
                    </nav>
                </div>
            </div>
            <div class="row">
                <div class="col-md-10 col-sm-11 mx-auto mt-4 text-center">
                    <div v-for="(name, index) in steps" :key="index" v-if="stepIsActive(index)">
                        <slot :name="`content_${index}`"/>
                    </div>
                </div>
            </div>
            <div class="row mt-5 mb-5 navigation-buttons">
                <div class="col text-right">
                    <button class="btn btn-light" v-if="hasPrevStep()" v-on:click="prevStep">< Avant
                    </button>
                </div>
                <div class="col text-left">
                    <button class="btn btn-light" v-if="hasNextStep()" v-on:click="nextStep">Après ></button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            steps: Array
        },
        data: function () {
            return {
                stepIndex: 0
            }
        },
        mounted() {
        },
        methods: {
            stepIsActive: function (index) {
                return this.stepIndex === index;
            },
            nextStep: function () {
                this.stepIndex++;
            },
            prevStep: function () {
                this.stepIndex--;
            },
            setStepIfAllowed: function (index) {
                if ((this.steps[index - 1] && this.steps[index - 1].allowNext) || index < this.stepIndex)
                    this.stepIndex = index;
            },
            hasPrevStep: function () {
                return this.stepIndex > 0;
            },
            hasNextStep: function () {
                return (this.stepIndex < (this.steps.length - 1));
            }
        }
    }
</script>
<style lang="scss">
    .navigation-buttons {
        .btn {
            color: #f44336;
            border: none;
            padding: 0.5rem;
            width: 150px;
            font-size: 1.2rem;
        }
    }

    .breadcrumb-item.no-icon::before {
        content: "";
    }

    .breadcrumbs {

        .breadcrumb {
            background: transparent;
        }

        .breadcrumb-item {
            font-size: 1.2rem;
            font-weight: 300;
            color: #B39DDB;
        }

        .breadcrumb-item.active {
            font-weight: 500;
            color: #3F51B5;
        }

        a {
            color: #f44336;
        }
    }

    .breadcrumb-item + .breadcrumb-item::before {
        display: none !important;
    }
</style>
