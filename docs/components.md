# Biblioteca de Componentes

## Introducción
Esta biblioteca de componentes está construida sobre shadcn/ui y TailwindCSS, proporcionando una colección de componentes reutilizables y accesibles para Te Lo Tengo.

## Principios de Diseño
1. **Accesibilidad**: Todos los componentes siguen las pautas WCAG 2.1
2. **Responsividad**: Diseño mobile-first con soporte para todos los tamaños de pantalla
3. **Personalización**: Temas y variantes configurables
4. **Rendimiento**: Optimizados para carga y renderizado

## Componentes Base

### Button
```tsx
import { Button } from '@/components/ui/button';

// Variantes
<Button variant="default">Default</Button>
<Button variant="destructive">Destructive</Button>
<Button variant="outline">Outline</Button>
<Button variant="secondary">Secondary</Button>
<Button variant="ghost">Ghost</Button>
<Button variant="link">Link</Button>

// Tamaños
<Button size="default">Default</Button>
<Button size="sm">Small</Button>
<Button size="lg">Large</Button>
<Button size="icon">Icon</Button>

// Estados
<Button disabled>Disabled</Button>
<Button loading>Loading</Button>
```

### Input
```tsx
import { Input } from '@/components/ui/input';

// Básico
<Input placeholder="Enter text..." />

// Con label
<div className="space-y-2">
  <Label htmlFor="email">Email</Label>
  <Input id="email" type="email" placeholder="name@example.com" />
</div>

// Con error
<Input error="Invalid email address" />

// Con icono
<div className="relative">
  <Input placeholder="Search..." />
  <SearchIcon className="absolute right-3 top-1/2 -translate-y-1/2" />
</div>
```

### Card
```tsx
import { Card } from '@/components/ui/card';

<Card>
  <CardHeader>
    <CardTitle>Title</CardTitle>
    <CardDescription>Description</CardDescription>
  </CardHeader>
  <CardContent>Content</CardContent>
  <CardFooter>Footer</CardFooter>
</Card>
```

### Toast
```tsx
import { useToast } from '@/hooks/use-toast';

const { toast } = useToast();

// Éxito
toast({
  title: 'Success',
  description: 'Operation completed successfully',
  variant: 'default',
});

// Error
toast({
  title: 'Error',
  description: 'Something went wrong',
  variant: 'destructive',
});
```

## Layouts

### MainLayout
```tsx
import { MainLayout } from '@/components/layouts';

<MainLayout>
  <h1>Page Content</h1>
</MainLayout>
```

### AuthLayout
```tsx
import { AuthLayout } from '@/components/layouts';

<AuthLayout>
  <LoginForm />
</AuthLayout>
```

### MarketplaceLayout
```tsx
import { MarketplaceLayout } from '@/components/layouts';

<MarketplaceLayout sidebar={<FilterSidebar />}>
  <ProductGrid />
</MarketplaceLayout>
```

## Componentes de Carga

### Loading
```tsx
import { Loading } from '@/components/ui/loading';

// Tamaños
<Loading size="sm" />
<Loading size="default" />
<Loading size="lg" />

// Pantalla completa
<Loading fullScreen />
```

### Skeleton
```tsx
import { Skeleton } from '@/components/ui/skeleton';

<Skeleton className="h-12 w-12 rounded-full" /> // Avatar
<Skeleton className="h-4 w-[250px]" /> // Texto
<Skeleton className="h-[200px] w-full rounded-lg" /> // Imagen
```

## Mejores Prácticas

### Composición
```tsx
// ✅ Bueno: Componentes pequeños y composables
<Card>
  <CardHeader>
    <CardTitle>Product</CardTitle>
    <CardDescription>Description</CardDescription>
  </CardHeader>
  <CardContent>
    <ProductDetails />
  </CardContent>
  <CardFooter>
    <Button>Buy Now</Button>
  </CardFooter>
</Card>

// ❌ Malo: Componentes monolíticos
<ProductCard title="Product" description="Description" price={100} />
```

### Props
```tsx
// ✅ Bueno: Props tipadas y documentadas
interface ButtonProps extends React.ButtonHTMLAttributes<HTMLButtonElement> {
  /** Indica si el botón está en estado de carga */
  loading?: boolean;
  /** Variante visual del botón */
  variant?: 'default' | 'destructive' | 'outline';
}

// ❌ Malo: Props sin tipos o documentación
interface ButtonProps {
  [key: string]: any;
}
```

### Accesibilidad
```tsx
// ✅ Bueno: Atributos ARIA y roles
<Button
  aria-label="Close dialog"
  role="button"
  onClick={closeDialog}
>
  <CloseIcon />
</Button>

// ❌ Malo: Sin consideraciones de accesibilidad
<div onClick={closeDialog}>
  <CloseIcon />
</div>
```

## Guías de Contribución
1. Todos los componentes deben tener:
   - TypeScript types
   - Tests unitarios
   - Documentación de props
   - Ejemplos de uso
   - Consideraciones de accesibilidad

2. Proceso de revisión:
   - Revisión de código
   - Pruebas de accesibilidad
   - Pruebas de rendimiento
   - Pruebas en diferentes dispositivos 