# new
```js
// Layout.vue
<keep-alive>
            <router-view
              v-if="render"
              ref="routerView"
              :key="
                getMicroApp($route.fullPath)
                  ? decodeURI($route.fullPath)
                  : decodeURI($route.fullPath)
              "
              @tab-open="openTab"
              @tab-close="closeTab"
            />
 </keep-alive>
// mount 方法          
this.$nextTick(() => {
      this.setRouterCaches(this.$refs.routerView.$vnode.parent.componentInstance)
      window.console.log(this.$refs.routerView.$vnode.parent.componentInstance)
    })
```
