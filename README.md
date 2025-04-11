## Next.js App Router Course - Starter

This is the starter template for the Next.js App Router Course. It contains the starting code for the dashboard application.

For more information, see the [course curriculum](https://nextjs.org/learn) on the Next.js Website.

## css
tailwind: css框架，定义了很多类名，就像添加在元素上的css类名一样，可直接添加在元素上。
css Modules：为组件创建作用域css,不会发生样式冲突。
clsx：可以让你轻松切换css类名。可以把clsx看做一个函数，它接受字符串或对象类型的参数，字符串就是tailwind类，对象是根据条件确定的tailwind类。

## 字体
使用`next/font/google`导入字体，然后指定字体的子集subset
```typescript
import { Inter } from 'next/font/google'
export const inter = Inter({sebsets: ['latin']})

//在组件中应用字体
import {inter} from "@/app/ui/fonts"
<p className={`${inter.className} text-xl`}>
```
## 图片
nextjs提供了Image组件，使用该组件加载图片可实现图片懒加载，防止图片在加载时发生布局跳动，在不通屏幕的设备间重新调整图片大小等特点。
```typescript
import Image from 'next/image'

export default function Page() {
    return (
        <Image 
          src="/"
          width={1000}
          height={760}
          className="hidden md:block"
        />
    )
}
```

## 路由
每一个文件夹就是一个嵌套路由，映射一个URL片段。

在nextjs中，page.tsx是一个可以导出React组件的特殊文件，是路由可被访问的必须文件。只有在page文件中的内容才能被公开访问，这一点和vue中的路由是一样的，在vue中只有和路由片段对应的文件才能被访问。

layout.tsx各子路由之间的共享UI，这一点和vue不同，在vue中共享UI写在一个文件中，这个文件映射一个路由片段，然后使用<router-view />来渲染不同的子路由对应的UI。

root layout就想vue中的app.js文件，所有的路由文件可共享。

## 页面之间的导航
### <Link />组件
使用<Link />组件进行路由之间导航，每次切换路由时页面只会局部重新渲染，而不会整个页面重新渲染。使用<Link />组件还有一个好处就是页面中的<Link />组件可以实现会预请求，当激活某个<Link />时，对应的文件已经在后台加载完成了。

### 获取当前路由路径
`import usePathname from 'next/navigation'`,使用usePathname()可以获取当前路由path.

## 静态渲染和动态渲染
对于静态渲染，在构建阶段或数据重新验证时，数据获取或页面渲染是在服务器上发生的。一些共享数据可以使用静态渲染。

对于动态渲染，每一个用户的请求内容都将在服务器上渲染。
动态渲染有以下好处：
1- 实时更新数据
2- 根据不同用户的数据渲染内容
3- 能够获取只有在请求时才能知道的信息

## streaming流式传输
流式传输是一种数据传输技术，它允许你将一个路径分解成更小的数据块，并在这些数据块准备就绪后，逐步从服务器传输到客户端。

在nextjs中，有两个方式执行流式传输：
1- 在页面层，创建一个loading.tsx文件，它能为你创建一个`<Suspense>`
2- 在组件层，使用`<Suspense>`进行颗粒度地控制
