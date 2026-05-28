# Next.js App Router Course - Starter

Run `pnpm i` to install the project's packages.

Followed by `pnpm dev` to start the development server.

`pnpm dev` starts your Next.js development server on `port 3000`

---

## Styling

When you use create-next-app to start a new project, Next.js will ask if you want to use Tailwind. If you select `yes`, **Next.js** will automatically install the necessary packages and configure **Tailwind** in your application.

**Tailwind** and **CSS** modules are the two most common ways of styling Next.js applications.

/app/ui/home.module.css

```css
.shape {
  height: 0;
  width: 0;
  border-bottom: 30px solid black;
  border-left: 20px solid transparent;
  border-right: 20px solid transparent;
}
```

/app/page.tsx

```typescript


import AcmeLogo from '@/app/ui/acme-logo';
import { ArrowRightIcon } from '@heroicons/react/24/outline';
import Link from 'next/link';
import styles from '@/app/ui/home.module.css';

export default function Page() {
  return (
    <main className="flex min-h-screen flex-col p-6">
      <div className={styles.shape} />
    // ...
  )
}
```

`clsx` is a library that lets you toggle class names easily.

/app/ui/invoices/status.tsx

```typescript


import clsx from 'clsx';

export default function InvoiceStatus({ status }: { status: string }) {
  return (
    <span
      className={clsx(
        'inline-flex items-center rounded-full px-2 py-1 text-sm',
        {
          'bg-gray-100 text-gray-500': status === 'pending',
          'bg-green-500 text-white': status === 'paid',
        },
      )}
    >
    // ...
)}

```

> Take a look at the [CSS documentation](https://nextjs.org/docs/app/getting-started/css) for more information.

### Fonts

**Next.js** automatically optimizes fonts in the application when you use the next/font module. It downloads font files at build time and hosts them with your other static assets. This means when a user visits your application, there are no additional network requests for fonts which would impact performance.

/app/iu / fonts.ts;

```typescript
import { Inter, Lusitana } from "next/font/google";

export const inter = Inter({ subsets: ["latin"] });

export const lusitana = Lusitana({
  weight: ["400", "700"],
  subsets: ["latin"],
});
```

/app/layout.tsx;

```tsx
import "@/app/ui/global.css";
import { inter } from "@/app/ui/fonts";

export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en">
      <body className={`${inter.className} antialiased`}>{children}</body>
    </html>
  );
}
```

### Images

**Next.js** can serve static assets, like images, under the top-level `/public` folder. Files inside `/public` can be referenced in your application.

With regular HTML, you would add an image as follows:

```html
<img
  src="/hero.png"
  alt="Screenshots of the dashboard project showing desktop version"
/>
```

However, this means you have to manually:

- Ensure your image is responsive on different screen sizes.
- Specify image sizes for different devices.
- Prevent layout shift as the images load.
- Lazy load images that are outside the user's viewport.

Images without dimensions and web fonts are common causes of layout shift due to the browser having to download additional resources.

Instead of manually implementing these optimizations, you can use the `next/image` component to automatically optimize your images.

**The `<Image>` component**
The `<Image>` Component is an extension of the HTML `<img>` tag, and comes with automatic image optimization, such as:

- Preventing layout shift automatically when images are loading.
- Resizing images to avoid shipping large images to devices with a smaller viewport.
- Lazy loading images by default (images load as they enter the viewport).
- Serving images in modern formats, like WebP and AVIF, when the browser supports it.

/app/page.tsx

```typescript
import AcmeLogo from '@/app/ui/acme-logo';
import { ArrowRightIcon } from '@heroicons/react/24/outline';
import Link from 'next/link';
import { lusitana } from '@/app/ui/fonts';
import Image from 'next/image';

export default function Page() {
  return (
    // ...
    <div className="flex items-center justify-center p-6 md:w-3/5 md:px-28 md:py-12">
      {/* Add Hero Images Here */}
      <Image
        src="/hero-desktop.png"
        width={1000}
        height={760}
        className="hidden md:block"
        alt="Screenshots of the dashboard project showing desktop version"
      />
    </div>
    //...
  );
}

```

It's good practice to set the `width` and `height` of your images to avoid layout shift, these should be an aspect ratio identical to the source image. These values are _not_ the size the image is rendered, but instead the size of the actual image file used to understand the aspect ratio.

Notice the class hidden to remove the image from the DOM on mobile screens, and md:block to show the image on desktop screens.

---

## Routing

### Nested routing

**Next.js** uses file-system routing where **folders** are used to create nested routes. Each folder represents a **route segment** that maps to a **URL segment.**

In this application, you already have a page file: `/app/page.tsx` - this is the home page associated with the route `/`.

You can create separate UIs for each route using `layout.tsx` and `page.tsx` files.

`page.tsx` is a special **Next.js** file that exports a React component, and it's required for the route to be accessible.

`app/dashboard/page.tsx`

`app/dashboard/invoices/page.tsx`

Dashboards have some sort of navigation that is shared across multiple pages. In Next.js, you can use a special `layout.tsx` file to create UI that is shared between multiple pages.

`/app/dashboard/layout.tsx`

One benefit of using layouts in **Next.js** is that on navigation, only the page components update while the layout won't re-render. This is called partial rendering which preserves client-side React state in the layout when transitioning between pages.

## Root Layout

A root `layout` is required in every **Next.js** application. Any UI you add to the root layout will be shared across all pages in your application. You can use the root layout to modify your `<html>` and `<body>` tags, and add metadata.

Since the new layout you've just created (`/app/dashboard/layout.tsx`) is unique to the `dashboard` pages, you don't need to add any UI to the root layout above.

---

This is the starter template for the Next.js App Router Course. It contains the starting code for the dashboard application.

For more information, see the [course curriculum](https://nextjs.org/learn) on the Next.js Website.
