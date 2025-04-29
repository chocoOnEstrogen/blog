---
title: "Next.js and TypeScript: Best Practices for 2025"
description: "Learn the latest best practices for building type-safe, performant Next.js applications with TypeScript"
date: "2025-04-29"
tags: "nextjs, typescript, web development, performance, best practices"
---

# Next.js and TypeScript: Best Practices for 2025

In the ever-evolving landscape of web development, Next.js and TypeScript have emerged as a powerful combination for building modern, type-safe applications. This post explores the latest best practices for 2025, helping you write more maintainable and performant code.

## 1. Type-Safe API Routes

Next.js 13+ introduced the App Router, which brings improved type safety to API routes. Here's how to leverage it:

```typescript
// app/api/hello/route.ts
import { NextRequest, NextResponse } from 'next/server'

interface RequestBody {
  name: string
  age: number
}

export async function POST(request: NextRequest) {
  try {
    const body: RequestBody = await request.json()
    
    return NextResponse.json({
      message: `Hello ${body.name}! You are ${body.age} years old.`
    })
  } catch (error) {
    return NextResponse.json(
      { error: 'Invalid request body' },
      { status: 400 }
    )
  }
}
```

## 2. Server Components and Type Safety

Server Components are a game-changer for performance. Here's how to use them effectively:

```typescript
// app/components/UserProfile.tsx
import { User } from '@/types'

interface UserProfileProps {
  userId: string
}

async function UserProfile({ userId }: UserProfileProps) {
  const user = await fetchUser(userId) // Type-safe database query
  
  return (
    <div>
      <h1>{user.name}</h1>
      <p>{user.bio}</p>
    </div>
  )
}
```

## 3. Optimized Image Handling

Next.js Image component with TypeScript:

```typescript
import Image from 'next/image'

interface HeroImageProps {
  src: string
  alt: string
  priority?: boolean
}

export function HeroImage({ src, alt, priority = false }: HeroImageProps) {
  return (
    <Image
      src={src}
      alt={alt}
      width={1200}
      height={630}
      priority={priority}
      className="rounded-lg"
    />
  )
}
```

## 4. Type-Safe Environment Variables

Using Zod for runtime type checking:

```typescript
// env.mjs
import { z } from 'zod'

const envSchema = z.object({
  DATABASE_URL: z.string().url(),
  NODE_ENV: z.enum(['development', 'production', 'test']),
  API_KEY: z.string().min(1),
})

export const env = envSchema.parse(process.env)
```

## 5. Performance Optimization

Implementing React.memo with TypeScript:

```typescript
import { memo } from 'react'

interface ExpensiveComponentProps {
  data: Array<{
    id: string
    value: number
  }>
  onUpdate: (id: string, value: number) => void
}

const ExpensiveComponent = memo<ExpensiveComponentProps>(
  ({ data, onUpdate }) => {
    // Component logic
  },
  (prevProps, nextProps) => {
    return prevProps.data === nextProps.data
  }
)
```

## 6. Error Handling

Type-safe error boundaries:

```typescript
'use client'

import { Component, ErrorInfo, ReactNode } from 'react'

interface Props {
  children: ReactNode
  fallback: ReactNode
}

interface State {
  hasError: boolean
}

class ErrorBoundary extends Component<Props, State> {
  public state: State = {
    hasError: false
  }

  public static getDerivedStateFromError(): State {
    return { hasError: true }
  }

  public componentDidCatch(error: Error, errorInfo: ErrorInfo) {
    console.error('Uncaught error:', error, errorInfo)
  }

  public render() {
    if (this.state.hasError) {
      return this.props.fallback
    }

    return this.props.children
  }
}
```

## Conclusion

By following these best practices, you can build more robust, type-safe, and performant Next.js applications. Remember to:

- Use TypeScript's strict mode
- Leverage server components where possible
- Implement proper error boundaries
- Optimize images and assets
- Use type-safe environment variables
- Implement proper caching strategies

Stay tuned for more tips and tricks in future posts!