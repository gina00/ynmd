# path路径方案
```
<el-alert
          v-if="projectId == '0'"
          title="您当前没有项目权限，请联系管理员配置！"
          type="success"
          center
          :closable="false"
        >
        </el-alert>
		
		<empty slot="empty">
        {{ !projectId || projectId == '0' ? '您当前没有项目权限，请联系管理员配置！' : '暂无数据' }}
      </empty>
	  
	  
	  
	  
	  
	 ----------------------- main.js----------------------------
	  
// let toPath = null
      // debugger
      // const ActiveWhen = pathToReg('/school/:id/class/:classId')
      // const toPath1 = ActiveWhen('/school/1/class/101')
      // const toPath2 = ActiveWhen('/school/1/classs/101')
      // for (let key in store.state.paths) {
      //   debugger
      //   if (to.path.startsWith(key)) {
      //     toPath = to.path.split('/:')[0]
      //   }
      //   // toPath=pathToActiveWhen(key)
      // }
      // console.log(toPath)
	  
	  
	 ------------------- qiankunConfig.js-----------------------
	  
	  
	  function pathToReg(path, exactMatch) {
  var regex = toDynamicPathValidatorRegex(path, exactMatch)
  return function(location) {
    // compatible with IE10
    var origin = location.origin

    if (!origin) {
      origin = ''.concat(location.protocol, '//').concat(location.host)
    }

    var route = location.href
      .replace(origin, '')
      .replace(location.search, '')
      .split('?')[0]
    return regex.test(route)
  }
}

function toDynamicPathValidatorRegex(path, exactMatch) {
  var lastIndex = 0,
    inDynamic = false,
    regexStr = '^'

  if (path[0] !== '/') {
    path = '/' + path
  }

  for (var charIndex = 0; charIndex < path.length; charIndex++) {
    var char = path[charIndex]
    var startOfDynamic = !inDynamic && char === ':'
    var endOfDynamic = inDynamic && char === '/'

    if (startOfDynamic || endOfDynamic) {
      appendToRegex(charIndex)
    }
  }

  appendToRegex(path.length)
  return new RegExp(regexStr, 'i')

  function appendToRegex(index) {
    var anyCharMaybeTrailingSlashRegex = '[^/]+/?'
    var commonStringSubPath = escapeStrRegex(path.slice(lastIndex, index))
    regexStr += inDynamic ? anyCharMaybeTrailingSlashRegex : commonStringSubPath

    if (index === path.length) {
      if (inDynamic) {
        if (exactMatch) {
          // Ensure exact match paths that end in a dynamic portion don't match
          // urls with characters after a slash after the dynamic portion.
          regexStr += '$'
        }
      } else {
        // For exact matches, expect no more characters. Otherwise, allow
        // any characters.
        var suffix = exactMatch ? '' : '.*'
        regexStr = // use charAt instead as we could not use es6 method endsWith
          regexStr.charAt(regexStr.length - 1) === '/'
            ? ''.concat(regexStr).concat(suffix, '$')
            : ''.concat(regexStr, '(/').concat(suffix, ')?(#.*)?$')
      }
    }

    inDynamic = !inDynamic
    lastIndex = index
  }

  function escapeStrRegex(str) {
    return str.replace(/[|\\{}()[\]^$+*?.]/g, '\\$&')
  }
}
```
