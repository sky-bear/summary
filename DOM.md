### DOM

### 遍历

- 查询父级

  ```js
  function parent(elem) {
      const parent = elem.parentNode
      return parent && parent.nodeType !== 11 ? parent : null
  }
  ```

- 查询父级列表

  ```js
  function parents(elem) {
      const matched = []
      while ((elem = elem['parentNode']) && elem.nodeType !== 9) {
          if (elem.nodeType === 1) {
              matched.push(elem)
          }
      }
      return matched
  }
  ```

- 查询父级列表直到对应的条件

  ```js
  function parentsUntil(elem, filter) {
      const matched = []
      while ((elem = elem['parentNode']) && elem.nodeType !== 9) {
          if (elem.nodeType === 1) {
              console.log(elem, elem.nodeName.toLowerCase())
              if (!!filter && elem.nodeName.toLowerCase() === filter) {
                  break
              }
              matched.push(elem)
          }
      }
      return matched
  }
  ```

- 查询匹配元素后面的所有同辈元素

  ```js
  function dir(elem, dir, until) {
      const matched = []
      while ((elem = elem[dir]) && elem.nodeType !== 9) {
          if (elem.nodeType === 1) {
              if (typeof until !== 'undefined') {
                  if (
                      elem.nodeName.toLowerCase() === until ||
                      [...elem.classList].includes(until)
                  ) {
                      break
                  }
              }
  
              matched.push(elem)
          }
      }
      return matched
  }
  
  function nextAll(elem) {
      return dir(elem, 'nextSibling')
  }
  
  function prevAll(elem) {
      return dir(elem, 'previousSibling')
  }
  
  function nextUntil(elem, until) {
      return dir(elem, 'nextSibling', until)
  }
  
  function prevUntil(elem, until) {
      return dir(elem, 'previousSibling', until)
  }
  ```

- 查询匹配元素前面的所有同辈元素

- 查询匹配元素后面的所有同辈元素，直到对应的条件

- 查询匹配元素前面的所有同辈元素，直到对应的条件