<template>
    <div class="vuefinder-file-content">
        <div class="vuefinder-file-icon">
            <span class="vuefinder-icon">
                <font-awesome-icon :icon="icon"></font-awesome-icon>
            </span>
        </div>

        <div class="vuefinder-file-name">
            <slot></slot>
        </div>
    </div>
</template>

<script>
    import {library} from '@fortawesome/fontawesome-svg-core'
    import {fas} from '@fortawesome/free-solid-svg-icons'
    import {FontAwesomeIcon} from '@fortawesome/vue-fontawesome'

    library.add(fas)

    export default {
        components: {FontAwesomeIcon},
        props: ['icon'],
        name: "FileIcon"
    }
</script>

<style lang="scss" scoped>
    .vuefinder-file-content {
        width: 100px;
        margin: 4px;
        display: flex;
        cursor: pointer;
        flex-direction: column;
        &:hover .vuefinder-file-name span:first-child {
            background-color: #e9ecf2;
        }
        &.node-selected .vuefinder-file-name span:first-child {
            background-color: #397fd5;
            color: #FFF;
            border: 1px solid transparent;
        }
    }

    .vuefinder-icon {
        display: inline-flex;
        margin: auto;
        justify-content: center;
        height: 3rem;
        width: 3rem;
        font-size: 3em;
        color: #66909e;
    }

    .vuefinder-file-icon {
        display: flex;
        margin-top: 5px;
        align-self: center;
        justify-content: flex-start;
    }

    .vuefinder-file-name {
        display: flex;
        margin-top: 5px;
        font-size: 12px;
        line-height: 24px;
        align-items: flex-start;
        flex: 1;
        justify-content: flex-start;

        span:first-child {
            flex: 1;
        }

        span {
            padding-left: 5px;
            padding-right: 5px;
            border-radius: 5px;
            text-align: center;
            word-break: break-all;
            border: 1px dashed transparent;
            &.selectable {
                border: 1px dashed #c5bebe;
            }
        }
    }

    .list {
        .vuefinder-file-content {
            width: auto;
            margin: 3px;
            flex-direction: row;
        }

        .vuefinder-icon {
            height: 1.5rem;
            width: 1.5rem;
            font-size: inherit;
            align-items: center;
        }

        .vuefinder-file-name {
            min-width: 0;

            span {
                text-align: left;
                overflow: hidden;
                text-overflow: ellipsis;
                white-space: nowrap;
            }
        }
    }

</style>