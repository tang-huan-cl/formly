
###  react-hook-form 

非常流行，号称业界性能第一的表单方案，我们看看它最简单的案例：

```js
import React from 'react'
import ReactDOM from 'react-dom'
import { useForm } from 'react-hook-form'
 
function App() {
  const { register, handleSubmit, errors } = useForm() // initialize the hook
  const onSubmit = (data) => {
    console.log(data)
  }
 
  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input name="firstname" ref={register} /> {/* register an input */}
      <input name="lastname" ref={register({ required: true })} />
      {errors.lastname && 'Last name is required.'}
      <input name="age" ref={register({ pattern: /\d+/ })} />
      {errors.age && 'Please enter number for age.'}
      <input type="submit" />
    </form>
  )
}
 
ReactDOM.render(<App />, document.getElementById('root'))
```

虽然值管理做到了精确渲染，但是在触发校验的时候，还是会导致表单全量渲染，因为 errors 状态的更新，是必须要整体受控渲染才能实现同步，这仅仅只是校验会全量渲染，其实还有联动，react-hook-form 要实现联动，同样是需要整体受控渲染才能实现联动。所以，如果要真正实现精确渲染，非 Reactive 不可！





