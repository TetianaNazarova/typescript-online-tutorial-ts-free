# typescript-online-tutorial-ts-free
TYPESCRIPT TS Online Tutorial
https://weblearn.my/ts-typescript-learning-typescript-ts-for-react-js-angular-vue-node-js/

# TypeScript Online Tutorial: Complete Developer's Guide to Mastering TypeScript

Learn TypeScript from zero to hero with this comprehensive online tutorial. Master static typing, advanced features, and framework integration for React, Angular, Vue, and Node.js development in 2025.

## Table of Contents

- [Why Choose TypeScript Over JavaScript?](#why-choose-typescript-over-javascript)
- [TypeScript Fundamentals](#typescript-fundamentals)
- [Setting Up Your Development Environment](#setting-up-your-development-environment)
- [Core TypeScript Features](#core-typescript-features)
- [Object-Oriented Programming in TypeScript](#object-oriented-programming-in-typescript)
- [Advanced TypeScript Patterns](#advanced-typescript-patterns)
- [TypeScript with Modern Frameworks](#typescript-with-modern-frameworks)
- [Real-World Project Examples](#real-world-project-examples)
- [Testing TypeScript Applications](#testing-typescript-applications)
- [Deployment and Production](#deployment-and-production)

## Why Choose TypeScript Over JavaScript?

TypeScript has become the go-to choice for enterprise-level applications and modern web development. Here's why learning TypeScript online is crucial for your development career:

### **Developer Productivity Benefits**

```typescript
// JavaScript - Runtime errors are common
function calculateDiscount(price, discountPercent) {
    return price - (price * discountPercent / 100);
}

// This will cause runtime errors
calculateDiscount("100", "10"); // String concatenation instead of math
calculateDiscount(100); // undefined discountPercent

// TypeScript - Compile-time error detection
function calculateDiscount(price: number, discountPercent: number): number {
    return price - (price * discountPercent / 100);
}

// TypeScript catches these errors before runtime
// calculateDiscount("100", "10"); // Error: Argument of type 'string' is not assignable
// calculateDiscount(100); // Error: Expected 2 arguments, but got 1
```

### **Industry Adoption Statistics**

- **85% of Fortune 500 companies** use TypeScript for their web applications
- **40% faster debugging** compared to vanilla JavaScript
- **60% reduction in runtime errors** in production applications
- **Top choice** for React, Angular, and Vue.js projects

## TypeScript Fundamentals

### **Understanding Type System Basics**

TypeScript's type system is built on JavaScript but adds compile-time type checking:

```typescript
// Primitive types
let productName: string = "MacBook Pro";
let price: number = 1299.99;
let inStock: boolean = true;
let releaseDate: Date = new Date("2024-01-15");

// Type inference - TypeScript automatically detects types
let category = "Electronics"; // TypeScript infers this as string
let quantity = 50; // TypeScript infers this as number

// Arrays with specific types
let colors: string[] = ["Silver", "Space Gray", "Gold"];
let ratings: number[] = [4.5, 4.8, 4.2, 4.9];

// Tuple types for fixed-length arrays
let coordinate: [number, number] = [40.7128, -74.0060];
let nameAge: [string, number] = ["Alice", 30];
```

### **Working with Complex Types**

```typescript
// Enum for better code organization
enum OrderStatus {
    Pending = "PENDING",
    Processing = "PROCESSING",
    Shipped = "SHIPPED",
    Delivered = "DELIVERED",
    Cancelled = "CANCELLED"
}

// Using enums in functions
function updateOrderStatus(orderId: string, status: OrderStatus): void {
    console.log(`Order ${orderId} status updated to ${status}`);
}

updateOrderStatus("ORD-001", OrderStatus.Shipped);

// Union types for flexible parameters
type PaymentMethod = "credit_card" | "paypal" | "bank_transfer" | "crypto";

interface PaymentInfo {
    method: PaymentMethod;
    amount: number;
    currency: string;
    processingFee?: number; // Optional property
}

function processPayment(payment: PaymentInfo): string {
    const total = payment.amount + (payment.processingFee || 0);
    return `Processing ${payment.method} payment of ${total} ${payment.currency}`;
}
```

## Setting Up Your Development Environment

### **Quick Start Installation**

```bash
# Create a new project directory
mkdir typescript-tutorial
cd typescript-tutorial

# Initialize npm project
npm init -y

# Install TypeScript and essential tools
npm install -D typescript @types/node ts-node-dev

# Create TypeScript configuration
npx tsc --init

# Install popular development dependencies
npm install -D eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin prettier
```

### **Optimized tsconfig.json Setup**

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "ESNext",
    "moduleResolution": "node",
    "lib": ["ES2022", "DOM", "DOM.Iterable"],
    "allowJs": true,
    "outDir": "./dist",
    "rootDir": "./src",
    "strict": true,
    "noImplicitAny": true,
    "strictNullChecks": true,
    "strictFunctionTypes": true,
    "noImplicitReturns": true,
    "noFallthroughCasesInSwitch": true,
    "noImplicitOverride": true,
    "exactOptionalPropertyTypes": true,
    "esModuleInterop": true,
    "allowSyntheticDefaultImports": true,
    "experimentalDecorators": true,
    "emitDecoratorMetadata": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "declaration": true,
    "declarationMap": true,
    "sourceMap": true,
    "removeComments": true,
    "incremental": true,
    "tsBuildInfoFile": "./dist/.tsbuildinfo"
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "dist", "**/*.test.ts", "**/*.spec.ts"]
}
```

### **Development Scripts Configuration**

```json
{
  "scripts": {
    "dev": "ts-node-dev --respawn --transpile-only src/index.ts",
    "build": "tsc",
    "start": "node dist/index.js",
    "clean": "rimraf dist",
    "type-check": "tsc --noEmit",
    "lint": "eslint src/**/*.ts",
    "lint:fix": "eslint src/**/*.ts --fix",
    "format": "prettier --write src/**/*.ts"
  }
}
```

## Core TypeScript Features

### **Interface Design Patterns**

```typescript
// Basic interface with optional and readonly properties
interface User {
    readonly id: string;
    name: string;
    email: string;
    age?: number;
    preferences: UserPreferences;
}

interface UserPreferences {
    theme: "light" | "dark" | "auto";
    notifications: {
        email: boolean;
        push: boolean;
        sms: boolean;
    };
    language: string;
}

// Extending interfaces for specialized types
interface AdminUser extends User {
    permissions: string[];
    lastLogin: Date;
}

interface GuestUser extends Omit<User, "preferences"> {
    sessionId: string;
    expiresAt: Date;
}

// Function interfaces for callback definitions
interface EventHandler<T> {
    (event: T): void | Promise<void>;
}

interface ValidationResult {
    isValid: boolean;
    errors?: string[];
}

interface Validator<T> {
    (data: T): ValidationResult;
}
```

### **Generic Programming Mastery**

```typescript
// Generic repository pattern
interface Repository<T, K = string> {
    findById(id: K): Promise<T | null>;
    findAll(): Promise<T[]>;
    create(entity: Omit<T, 'id'>): Promise<T>;
    update(id: K, updates: Partial<T>): Promise<T>;
    delete(id: K): Promise<boolean>;
}

// Implementation example
class UserRepository implements Repository<User> {
    private users: User[] = [];

    async findById(id: string): Promise<User | null> {
        return this.users.find(user => user.id === id) || null;
    }

    async findAll(): Promise<User[]> {
        return [...this.users];
    }

    async create(userData: Omit<User, 'id'>): Promise<User> {
        const user: User = {
            id: crypto.randomUUID(),
            ...userData
        };
        this.users.push(user);
        return user;
    }

    async update(id: string, updates: Partial<User>): Promise<User> {
        const index = this.users.findIndex(user => user.id === id);
        if (index === -1) throw new Error('User not found');
        
        this.users[index] = { ...this.users[index], ...updates };
        return this.users[index];
    }

    async delete(id: string): Promise<boolean> {
        const index = this.users.findIndex(user => user.id === id);
        if (index === -1) return false;
        
        this.users.splice(index, 1);
        return true;
    }
}

// Generic API response wrapper
interface ApiResponse<T> {
    data: T;
    status: 'success' | 'error';
    message?: string;
    meta?: {
        page?: number;
        limit?: number;
        total?: number;
    };
}

// Generic API client
class ApiClient {
    private baseUrl: string;

    constructor(baseUrl: string) {
        this.baseUrl = baseUrl;
    }

    async get<T>(endpoint: string): Promise<ApiResponse<T>> {
        const response = await fetch(`${this.baseUrl}${endpoint}`);
        return response.json();
    }

    async post<T, D = unknown>(endpoint: string, data: D): Promise<ApiResponse<T>> {
        const response = await fetch(`${this.baseUrl}${endpoint}`, {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify(data)
        });
        return response.json();
    }
}
```

### **Utility Types Deep Dive**

```typescript
// Built-in utility types examples
interface Product {
    id: string;
    name: string;
    price: number;
    description: string;
    category: string;
    inStock: boolean;
}

// Partial - for update operations
type ProductUpdate = Partial<Product>;

function updateProduct(id: string, updates: ProductUpdate): Product {
    // Implementation here
    return {} as Product;
}

// Pick - select specific fields
type ProductSummary = Pick<Product, 'id' | 'name' | 'price'>;

// Omit - exclude specific fields
type CreateProductData = Omit<Product, 'id'>;

// Required - make all properties required
type CompleteProduct = Required<Product>;

// Record - create mapped types
type ProductsByCategory = Record<string, Product[]>;

// Custom utility types
type NonNullable<T> = T extends null | undefined ? never : T;
type DeepReadonly<T> = {
    readonly [P in keyof T]: T[P] extends object ? DeepReadonly<T[P]> : T[P];
};

// Conditional types for advanced type manipulation
type ApiEndpoint<T> = T extends 'users' 
    ? '/api/users' 
    : T extends 'products' 
    ? '/api/products' 
    : never;

type UserEndpoint = ApiEndpoint<'users'>; // '/api/users'
type ProductEndpoint = ApiEndpoint<'products'>; // '/api/products'
```

## Object-Oriented Programming in TypeScript

### **Classes and Inheritance**

```typescript
// Abstract base class
abstract class BaseEntity {
    protected readonly id: string;
    protected createdAt: Date;
    protected updatedAt: Date;

    constructor(id?: string) {
        this.id = id || crypto.randomUUID();
        this.createdAt = new Date();
        this.updatedAt = new Date();
    }

    abstract validate(): boolean;

    public getId(): string {
        return this.id;
    }

    public getCreatedAt(): Date {
        return this.createdAt;
    }

    protected touch(): void {
        this.updatedAt = new Date();
    }
}

// Concrete implementation
class Customer extends BaseEntity {
    private name: string;
    private email: string;
    private orders: Order[] = [];

    constructor(name: string, email: string, id?: string) {
        super(id);
        this.name = name;
        this.email = email;
    }

    validate(): boolean {
        return this.name.length > 0 && this.email.includes('@');
    }

    addOrder(order: Order): void {
        this.orders.push(order);
        this.touch();
    }

    getOrders(): ReadonlyArray<Order> {
        return [...this.orders];
    }

    // Getter and setter
    get customerName(): string {
        return this.name;
    }

    set customerName(value: string) {
        if (value.length < 2) {
            throw new Error('Name must be at least 2 characters');
        }
        this.name = value;
        this.touch();
    }
}

// Decorator example
function LogMethod(target: any, propertyKey: string, descriptor: PropertyDescriptor) {
    const originalMethod = descriptor.value;
    
    descriptor.value = function (...args: any[]) {
        console.log(`Calling ${propertyKey} with args:`, args);
        const result = originalMethod.apply(this, args);
        console.log(`${propertyKey} returned:`, result);
        return result;
    };
}

class OrderService {
    @LogMethod
    calculateTotal(items: OrderItem[]): number {
        return items.reduce((sum, item) => sum + item.price * item.quantity, 0);
    }
}
```

### **Mixins and Composition**

```typescript
// Mixin implementation
type Constructor = new (...args: any[]) => {};

function Timestamped<TBase extends Constructor>(Base: TBase) {
    return class extends Base {
        timestamp = new Date();
        
        getTimestamp() {
            return this.timestamp;
        }
    };
}

function Serializable<TBase extends Constructor>(Base: TBase) {
    return class extends Base {
        serialize(): string {
            return JSON.stringify(this);
        }
        
        static deserialize(json: string) {
            return JSON.parse(json);
        }
    };
}

// Using mixins
class SimpleProduct {
    constructor(public name: string, public price: number) {}
}

const EnhancedProduct = Serializable(Timestamped(SimpleProduct));

const product = new EnhancedProduct("Laptop", 999);
console.log(product.getTimestamp());
console.log(product.serialize());
```

## Advanced TypeScript Patterns

### **Module Augmentation and Declaration Merging**

```typescript
// Extending existing interfaces
declare global {
    interface Window {
        myCustomProperty: string;
    }
}

// Module augmentation for third-party libraries
declare module 'express' {
    interface Request {
        user?: User;
    }
}

// Declaration merging example
interface MergeExample {
    property1: string;
}

interface MergeExample {
    property2: number;
}

// Result: MergeExample has both property1 and property2
```

### **Template Literal Types**

```typescript
// Advanced template literal types
type HttpMethod = 'GET' | 'POST' | 'PUT' | 'DELETE';
type ApiVersion = 'v1' | 'v2';
type Resource = 'users' | 'products' | 'orders';

type ApiEndpoint = `/${ApiVersion}/${Resource}`;
type ApiUrl = `https://api.example.com${ApiEndpoint}`;

// Route parameter extraction
type ExtractRouteParams<T extends string> = 
    T extends `${infer _Start}:${infer Param}/${infer Rest}`
        ? { [K in Param | keyof ExtractRouteParams<Rest>]: string }
        : T extends `${infer _Start}:${infer Param}`
        ? { [K in Param]: string }
        : {};

type UserRouteParams = ExtractRouteParams<'/users/:id/posts/:postId'>;
// Result: { id: string; postId: string }
```

### **Mapped Types and Conditional Logic**

```typescript
// Recursive type transformation
type DeepPartial<T> = {
    [P in keyof T]?: T[P] extends object ? DeepPartial<T[P]> : T[P];
};

// Create form types from data types
type FormField<T> = {
    value: T;
    error?: string;
    touched: boolean;
    validate: (value: T) => string | undefined;
};

type FormData<T> = {
    [K in keyof T]: FormField<T[K]>;
};

// Usage
interface SignupData {
    username: string;
    email: string;
    age: number;
}

type SignupForm = FormData<SignupData>;
// Result: Each property becomes a FormField<T>
```

## TypeScript with Modern Frameworks

### **React with TypeScript Mastery**

```typescript
import React, { useState, useEffect, useCallback, useMemo } from 'react';

// Component props interface
interface ProductListProps {
    category?: string;
    onProductSelect: (product: Product) => void;
    loading?: boolean;
}

// Custom hooks with TypeScript
function useProducts(category?: string) {
    const [products, setProducts] = useState<Product[]>([]);
    const [loading, setLoading] = useState(true);
    const [error, setError] = useState<string | null>(null);

    const fetchProducts = useCallback(async () => {
        try {
            setLoading(true);
            const apiClient = new ApiClient('https://api.example.com');
            const response = await apiClient.get<Product[]>('/products');
            
            if (response.status === 'success') {
                setProducts(response.data);
            } else {
                setError(response.message || 'Failed to fetch products');
            }
        } catch (err) {
            setError(err instanceof Error ? err.message : 'Unknown error');
        } finally {
            setLoading(false);
        }
    }, []);

    useEffect(() => {
        fetchProducts();
    }, [fetchProducts, category]);

    return { products, loading, error, refetch: fetchProducts };
}

// React component with TypeScript
const ProductList: React.FC<ProductListProps> = ({ 
    category, 
    onProductSelect, 
    loading: externalLoading = false 
}) => {
    const { products, loading: dataLoading, error } = useProducts(category);
    
    const filteredProducts = useMemo(() => {
        if (!category) return products;
        return products.filter(product => product.category === category);
    }, [products, category]);

    const handleProductClick = useCallback((product: Product) => {
        onProductSelect(product);
    }, [onProductSelect]);

    if (dataLoading || externalLoading) {
        return <div className="loading">Loading products...</div>;
    }

    if (error) {
        return <div className="error">Error: {error}</div>;
    }

    return (
        <div className="product-list">
            {filteredProducts.map(product => (
                <ProductCard 
                    key={product.id}
                    product={product}
                    onClick={handleProductClick}
                />
            ))}
        </div>
    );
};

// Higher-order component with TypeScript
function withAuth<T extends object>(Component: React.ComponentType<T>) {
    return function AuthenticatedComponent(props: T) {
        const [user, setUser] = useState<User | null>(null);
        
        useEffect(() => {
            // Check authentication
            const checkAuth = async () => {
                // Implementation
            };
            checkAuth();
        }, []);

        if (!user) {
            return <div>Please log in</div>;
        }

        return <Component {...props} />;
    };
}
```

### **Node.js Backend with TypeScript**

```typescript
import express, { Request, Response, NextFunction } from 'express';
import { body, validationResult, ValidationChain } from 'express-validator';

// Request/Response type augmentation
interface AuthenticatedRequest extends Request {
    user: User;
}

// Validation middleware with TypeScript
const validateRequest = (validations: ValidationChain[]) => {
    return async (req: Request, res: Response, next: NextFunction) => {
        await Promise.all(validations.map(validation => validation.run(req)));
        
        const errors = validationResult(req);
        if (!errors.isEmpty()) {
            return res.status(400).json({ errors: errors.array() });
        }
        
        next();
    };
};

// Service layer with dependency injection
interface UserService {
    createUser(userData: CreateUserData): Promise<User>;
    getUserById(id: string): Promise<User | null>;
    updateUser(id: string, updates: Partial<User>): Promise<User>;
}

class UserServiceImpl implements UserService {
    constructor(private userRepository: Repository<User>) {}

    async createUser(userData: CreateUserData): Promise<User> {
        const user = await this.userRepository.create(userData);
        // Send welcome email, etc.
        return user;
    }

    async getUserById(id: string): Promise<User | null> {
        return this.userRepository.findById(id);
    }

    async updateUser(id: string, updates: Partial<User>): Promise<User> {
        return this.userRepository.update(id, updates);
    }
}

// Controller with proper error handling
class UserController {
    constructor(private userService: UserService) {}

    createUser = async (req: Request, res: Response, next: NextFunction) => {
        try {
            const user = await this.userService.createUser(req.body);
            res.status(201).json({ data: user, status: 'success' });
        } catch (error) {
            next(error);
        }
    };

    getUser = async (req: Request, res: Response, next: NextFunction) => {
        try {
            const user = await this.userService.getUserById(req.params.id);
            if (!user) {
                return res.status(404).json({ 
                    status: 'error', 
                    message: 'User not found' 
                });
            }
            res.json({ data: user, status: 'success' });
        } catch (error) {
            next(error);
        }
    };
}

// Express app setup with TypeScript
const app = express();
const userRepository = new UserRepository();
const userService = new UserServiceImpl(userRepository);
const userController = new UserController(userService);

app.post('/users', 
    validateRequest([
        body('name').isLength({ min: 2 }).withMessage('Name must be at least 2 characters'),
        body('email').isEmail().withMessage('Valid email required'),
    ]),
    userController.createUser
);

app.get('/users/:id', userController.getUser);
```

### **Vue.js with TypeScript**

```typescript
import { defineComponent, ref, computed, onMounted, PropType } from 'vue';

// Component with TypeScript
export default defineComponent({
    name: 'ProductManager',
    props: {
        initialProducts: {
            type: Array as PropType<Product[]>,
            default: () => []
        },
        readonly: {
            type: Boolean,
            default: false
        }
    },
    emits: {
        'product-created': (product: Product) => true,
        'product-updated': (product: Product) => true,
        'product-deleted': (productId: string) => true
    },
    setup(props, { emit }) {
        const products = ref<Product[]>(props.initialProducts);
        const selectedProduct = ref<Product | null>(null);
        const searchQuery = ref('');

        const filteredProducts = computed(() => {
            if (!searchQuery.value) return products.value;
            return products.value.filter(product =>
                product.name.toLowerCase().includes(searchQuery.value.toLowerCase())
            );
        });

        const createProduct = async (productData: CreateProductData) => {
            const newProduct: Product = {
                id: crypto.randomUUID(),
                ...productData
            };
            products.value.push(newProduct);
            emit('product-created', newProduct);
        };

        const updateProduct = async (id: string, updates: Partial<Product>) => {
            const index = products.value.findIndex(p => p.id === id);
            if (index !== -1) {
                products.value[index] = { ...products.value[index], ...updates };
                emit('product-updated', products.value[index]);
            }
        };

        const deleteProduct = async (id: string) => {
            const index = products.value.findIndex(p => p.id === id);
            if (index !== -1) {
                products.value.splice(index, 1);
                emit('product-deleted', id);
            }
        };

        onMounted(() => {
            console.log('ProductManager mounted with', products.value.length, 'products');
        });

        return {
            products,
            selectedProduct,
            searchQuery,
            filteredProducts,
            createProduct,
            updateProduct,
            deleteProduct
        };
    }
});
```

## Real-World Project Examples

### **E-commerce API with TypeScript**

```typescript
// Domain models
interface Product {
    id: string;
    name: string;
    price: number;
    description: string;
    category: Category;
    inventory: InventoryInfo;
    images: string[];
    createdAt: Date;
    updatedAt: Date;
}

interface Category {
    id: string;
    name: string;
    parentId?: string;
}

interface InventoryInfo {
    quantity: number;
    reservedQuantity: number;
    lowStockThreshold: number;
}

interface Order {
    id: string;
    customerId: string;
    items: OrderItem[];
    status: OrderStatus;
    totalAmount: number;
    shippingAddress: Address;
    createdAt: Date;
}

interface OrderItem {
    productId: string;
    quantity: number;
    price: number;
}

// Business logic services
class OrderService {
    constructor(
        private orderRepository: Repository<Order>,
        private productService: ProductService,
        private inventoryService: InventoryService
    ) {}

    async createOrder(customerId: string, items: CreateOrderItem[]): Promise<Order> {
        // Validate inventory
        for (const item of items) {
            const available = await this.inventoryService.checkAvailability(
                item.productId, 
                item.quantity
            );
            if (!available) {
                throw new Error(`Insufficient inventory for product ${item.productId}`);
            }
        }

        // Calculate total
        const orderItems: OrderItem[] = [];
        let totalAmount = 0;

        for (const item of items) {
            const product = await this.productService.getById(item.productId);
            if (!product) {
                throw new Error(`Product ${item.productId} not found`);
            }

            const orderItem: OrderItem = {
                productId: item.productId,
                quantity: item.quantity,
                price: product.price
            };
            
            orderItems.push(orderItem);
            totalAmount += orderItem.price * orderItem.quantity;
        }

        // Create order
        const order: Omit<Order, 'id'> = {
            customerId,
            items: orderItems,
            status: OrderStatus.Pending,
            totalAmount,
            shippingAddress: item.shippingAddress,
            createdAt: new Date()
        };

        const createdOrder = await this.orderRepository.create(order);

        // Reserve inventory
        for (const item of orderItems) {
            await this.inventoryService.reserveQuantity(item.productId, item.quantity);
        }

        return createdOrder;
    }
}
```

### **Chat Application with TypeScript**

```typescript
// WebSocket server with TypeScript
import WebSocket from 'ws';

interface ChatMessage {
    id: string;
    roomId: string;
    userId: string;
    content: string;
    timestamp: Date;
    type: 'text' | 'image' | 'file';
}

interface ChatRoom {
    id: string;
    name: string;
    participants: string[];
    messages: ChatMessage[];
    createdAt: Date;
}

interface WebSocketClient extends WebSocket {
    userId?: string;
    roomId?: string;
}

class ChatServer {
    private wss: WebSocket.Server;
    private clients: Map<string, WebSocketClient> = new Map();
    private rooms: Map<string, ChatRoom> = new Map();

    constructor(port: number) {
        this.wss = new WebSocket.Server({ port });
        this.setupEventHandlers();
    }

    private setupEventHandlers(): void {
        this.wss.on('connection', (ws: WebSocketClient, req) => {
            console.log('New client connected');

            ws.on('message', (data: string) => {
                try {
                    const message = JSON.parse(data);
                    this.handleMessage(ws, message);
                } catch (error) {
                    ws.send(JSON.stringify({ 
                        type: 'error', 
                        message: 'Invalid JSON' 
                    }));
                }
            });

            ws.on('close', () => {
                this.handleDisconnection(ws);
            });
        });
    }

    private handleMessage(client: WebSocketClient, message: any): void {
        switch (message.type) {
            case 'join_room':
                this.joinRoom(client, message.roomId, message.userId);
                break;
            case 'send_message':
                this.broadcastMessage(client, message);
                break;
            case 'leave_room':
                this.leaveRoom(client);
                break;
        }
    }

    private joinRoom(client: WebSocketClient, roomId: string, userId: string): void {
        client.userId = userId;
        client.roomId = roomId;
        this.clients.set(userId, client);

        if (!this.rooms.has(roomId)) {
            this.rooms.set(roomId, {
                id: roomId,
                name: `Room ${roomId}`,
                participants: [],
                messages: [],
                createdAt: new Date()
            });
        }

        const room = this.rooms.get(roomId)!;
        if (!room.participants.includes(userId)) {
            room.participants.push(userId);
        }

        client.send(JSON.stringify({
            type: 'joined_room',
            roomId,
            messages: room.messages.slice(-50) // Send last 50 messages
        }));
    }

    private broadcastMessage(sender: WebSocketClient, messageData: any): void {
        if (!sender.roomId || !sender.userId) return;

        const chatMessage: ChatMessage = {
            id: crypto.randomUUID(),
            roomId: sender.roomId,
            userId: sender.userId,
            content: messageData.content,
            timestamp: new Date(),
            type: messageData.messageType || 'text'
        };

        const room = this.rooms.get(sender.roomId);
....

TYPESCRIPT TS Online Tutorial eBook, pdf, TypeScript course free
https://weblearn.my/ts-typescript-learning-typescript-ts-for-react-js-angular-vue-node-js/
