## 自定义过滤器


DynamicFilter


### 1 select组件优化


输入重复按回车键做保留处理、输入后不能删除

[参考地址](https://blog.csdn.net/weixin_44205785/article/details/108071393)


```js
 <Select
                mode="tags"
                onInputKeyDown={(e) => {
                  if (e.key === 'Enter' && e.target.value) {
                    const currentValue = e.target.value
                    const findValue = getFieldValue('test').indexOf(
                      currentValue
                    )
                    e.persist()
                    setTimeout(() => {
                      if (findValue !== -1) {
                        setFieldsValue({
                          test: [...getFieldValue('test'), currentValue],
                        })
                      }
                    })
                  }
                }}
```