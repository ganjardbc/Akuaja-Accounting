<template>
    <div id="AppTabs" class="tabs theme-1">
        <button 
            v-if="isScrollable" 
            class="tabs-button" 
            @click="toLeft(path ? path : 'nav-topic')">
            <i class="fa fa-lg fa-angle-left" />
        </button>
        <ul 
            :class="`
                tabs-content 
                ${isFull ? 'full' : ''}
            `" 
            :style="`
                width: ${isScrollable ? 'calc(100% - 70px)' : '100%'}; 
                overflow-x: auto;
            `"
            :id="path ? path : 'nav-topic'">
            <li 
                v-for="(dt, index) in datas" 
                :key="index" 
                :class="selectedIndex === index ? 'active' : ''"
                @click="onClick(index)">
                <div class="display-flex align-center center">
                    <div class="tabs-label">{{ dt.label }}</div>
                    <div v-if="dt.val" class="tabs-val">{{ dt.val }}</div>
                </div>
            </li>
        </ul>
        <button 
            v-if="isScrollable" 
            class="tabs-button" 
            @click="toRight(path ? path : 'nav-topic')">
            <i class="fa fa-lg fa-angle-right" />
        </button>
    </div>
</template>

<script>
export default {
    name: 'AppTabs',
    props: {
        path: {
            required: false
        },
        selectedIndex: {
            required: false
        },
        data: {
            required: true
        },
        isScrollable: {
            type: Boolean,
            required: false,
            default: false
        },
        isFull: {
            type: Boolean,
            required: false,
            default: false
        },
        onChange: {
            type: Function,
            required: false
        }
    },
    data () {
        return {
            index: 0,
            datas: this.data
        }
    },
    methods: {
        onClick: function (index) {
            let payload = this.datas && this.datas.map((dt, idx) => {
                return {
                    ...dt,
                    status: idx === index ? 'active' : ''
                }
            })
            this.datas = payload
            this.onChange(index)
        },
        toLeft: function (path) {
			var wd = $('#'+path).width()
			var sc = $('#'+path).scrollLeft()
			if (sc >= 0) {
				$('#'+path).animate({scrollLeft: (sc - wd)}, 500)
			}
		},
		toRight: function (path) {
			var wd = $('#'+path).width()
			var sc = $('#'+path).scrollLeft()
			if (true) {
				$('#'+path).animate({scrollLeft: (sc + wd)}, 500)
			}
		}
    },
    watch: {
        data: function (props) {
            this.datas = props 
        }
    }
}
</script>