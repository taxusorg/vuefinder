<template>
    <div class="vuefinder-header">
        <div class="vuefinder-breadcrumb">
            <div @click="$emit('openFolder',root)" class="vuefinder-breadcrumb-item">
                   <span class="icon">
                       <font-awesome-icon icon="home"></font-awesome-icon>
                   </span>
            </div>
        </div>
        <div v-for="(item, index) of breadcrumb" :key="index" class="vuefinder-breadcrumb">
            <div @click="$emit('openFolder',item.dirname)" class="vuefinder-breadcrumb-item">
                    <span v-if="item.length != 0">
                        {{ item.basename }}
                    </span>
            </div>
        </div>
        <div class="vuefinder-loader" v-show="loading">
                   <span class="icon">
                       <font-awesome-icon icon="spinner" spin></font-awesome-icon>
                   </span>
        </div>
    </div>
</template>

<script>
    import {library} from '@fortawesome/fontawesome-svg-core'
    import {fas} from '@fortawesome/free-solid-svg-icons'
    import {FontAwesomeIcon} from '@fortawesome/vue-fontawesome'

    library.add(fas)

    export default {
        props: ['root', 'dirname', 'loading'],
        name: "BreadcrumbHeader",
        components: {FontAwesomeIcon},
        computed: {
            breadcrumb: function () {
                let items = [], links = [],
                    root = '^' + this.root.replace(/([^\w ])/, '\\$1') + '\/?',
                    regex = new RegExp(root, "i"),
                    path = this.dirname.replace(regex, '');

                if (path.length == 0) {
                    return [];
                }
                path.split('/')
                    .forEach(function (item) {
                        items.push(item);
                        if (items.join('/') != '') {
                            links.push({
                                'basename': item,
                                'dirname': items.join('/'),
                                'type': 'folder'
                            });
                        }
                    });
                return links;
            }
        }
    }
</script>

<style lang="scss" scoped>
    .vuefinder-header {
        display: flex;
        background-color: #fbfcfd;
        border-bottom: 1px solid lightgray;
        border-top: 1px solid lightgray;
        font-size: 14px;
        font-weight: bold;
        flex-wrap: wrap;
        padding: 10px;

        .vuefinder-loader {
            flex: 1;
            text-align: right;
            display: flex;
            flex-direction: row-reverse;
            .icon {
                font-size: 1.2rem;
            }
        }

        .vuefinder-breadcrumb {
            display: flex;
            height: 25px;
            line-height: 28px;

            .vuefinder-breadcrumb-item {
                display: flex;
                padding-left: 5px;
                padding-right: 5px;
                cursor: pointer;
                color: #3a525a;
                transition: 0.2s;
                .icon {
                    font-size: 1.5rem;
                }
            }
            .vuefinder-breadcrumb-item:hover {
                color: #87a6af;

            }
        }
        .vuefinder-breadcrumb + .vuefinder-breadcrumb::before {
            content: ' / ';
        }
    }
</style>