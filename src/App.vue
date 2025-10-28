<template>
  <div class="vue-app">
    <!-- Toast Notification -->
    <Transition name="toast">
      <div
        v-if="toast"
        :class="[
          'fixed top-4 right-4 z-50 px-6 py-3 rounded-lg shadow-lg text-white',
          toast.type === 'success' ? 'bg-green-500' : 'bg-red-500',
        ]"
      >
        <div class="flex items-center gap-2">
          <span>{{ toast.message }}</span>
          <button @click="toast = null" class="ml-2 font-bold">×</button>
        </div>
      </div>
    </Transition>

    <!-- Landing Page -->
    <div
      v-if="currentView === 'landing'"
      class="min-h-screen bg-linear-to-br from-blue-50 to-indigo-50"
    >
      <div class="max-w-[1440px] mx-auto">
        <header class="flex justify-between items-center px-6 py-4">
          <h1 class="text-2xl font-bold text-indigo-600">TicketFlow Vue</h1>
          <button
            @click="navigateTo('login')"
            class="px-6 py-2 bg-indigo-600 text-white rounded-lg hover:bg-indigo-700 transition"
          >
            Login
          </button>
        </header>

        <section class="relative px-6 py-20 overflow-hidden">
          <div
            class="absolute top-10 right-20 w-64 h-64 bg-indigo-200 rounded-full opacity-20 blur-3xl"
          ></div>
          <div
            class="absolute bottom-20 left-10 w-48 h-48 bg-purple-200 rounded-full opacity-30"
          ></div>

          <div class="relative z-10 text-center max-w-4xl mx-auto">
            <h1 class="text-5xl md:text-6xl font-bold text-gray-900 mb-6">
              Manage Your Tickets
              <span class="text-indigo-600"> Effortlessly</span>
            </h1>
            <p class="text-xl text-gray-600 mb-8">
              Streamline your workflow with our powerful ticket management system
            </p>
            <div class="flex gap-4 justify-center flex-wrap">
              <button
                @click="navigateTo('signup')"
                class="px-8 py-3 bg-indigo-600 text-white rounded-lg hover:bg-indigo-700 transition text-lg font-semibold"
              >
                Get Started
              </button>
              <button
                @click="navigateTo('login')"
                class="px-8 py-3 bg-white text-indigo-600 rounded-lg border-2 border-indigo-600 hover:bg-indigo-50 transition text-lg font-semibold"
              >
                Login
              </button>
            </div>
          </div>

          <svg
            class="absolute bottom-0 left-0 w-full"
            viewBox="0 0 1440 320"
            preserveAspectRatio="none"
          >
            <path
              fill="#4F46E5"
              fill-opacity="0.1"
              d="M0,96L48,112C96,128,192,160,288,160C384,160,480,128,576,122.7C672,117,768,139,864,154.7C960,171,1056,181,1152,165.3C1248,149,1344,107,1392,85.3L1440,64L1440,320L1392,320C1344,320,1248,320,1152,320C1056,320,960,320,864,320C768,320,672,320,576,320C480,320,384,320,288,320C192,320,96,320,48,320L0,320Z"
            ></path>
          </svg>
        </section>

        <section class="px-6 py-16">
          <div class="grid md:grid-cols-3 gap-8 max-w-6xl mx-auto">
            <div
              v-for="(feature, i) in features"
              :key="i"
              class="bg-white p-8 rounded-2xl shadow-lg"
            >
              <h3 class="text-xl font-bold mb-3 text-gray-900">{{ feature.title }}</h3>
              <p class="text-gray-600">{{ feature.desc }}</p>
            </div>
          </div>
        </section>

        <footer class="px-6 py-8 border-t border-gray-200 text-center text-gray-600">
          <p>&copy; 2025 TicketFlow Vue. All rights reserved.</p>
        </footer>
      </div>
    </div>

    <!-- Auth Page -->
    <div
      v-if="currentView === 'login' || currentView === 'signup'"
      class="min-h-screen bg-linear-to-br from-blue-50 to-indigo-50 flex items-center justify-center px-6"
    >
      <div class="max-w-md w-full">
        <div class="bg-white rounded-2xl shadow-xl p-8">
          <h2 class="text-3xl font-bold text-gray-900 mb-6 text-center">
            {{ currentView === 'login' ? 'Welcome Back' : 'Create Account' }}
          </h2>
          <div class="space-y-4">
            <div>
              <label class="block text-sm font-medium text-gray-700 mb-1">Email</label>
              <input
                v-model="authForm.email"
                type="email"
                @keyup.enter="handleAuth"
                class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-transparent outline-none"
                placeholder="you@example.com"
              />
              <p v-if="authErrors.email" class="text-red-500 text-sm mt-1">
                {{ authErrors.email }}
              </p>
            </div>
            <div>
              <label class="block text-sm font-medium text-gray-700 mb-1">Password</label>
              <input
                v-model="authForm.password"
                type="password"
                @keyup.enter="handleAuth"
                class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-transparent outline-none"
                placeholder="••••••••"
              />
              <p v-if="authErrors.password" class="text-red-500 text-sm mt-1">
                {{ authErrors.password }}
              </p>
            </div>
            <button
              @click="handleAuth"
              class="w-full px-4 py-3 bg-indigo-600 text-white rounded-lg hover:bg-indigo-700 transition font-semibold"
            >
              {{ currentView === 'login' ? 'Log In' : 'Sign Up' }}
            </button>
          </div>
          <p class="mt-4 text-center text-gray-600">
            {{ currentView === 'login' ? "Don't have an account? " : 'Already have an account? ' }}
            <button
              @click="navigateTo(currentView === 'login' ? 'signup' : 'login')"
              class="text-indigo-600 font-semibold hover:underline"
            >
              {{ currentView === 'login' ? 'Sign Up' : 'Log In' }}
            </button>
          </p>
          <button
            @click="navigateTo('landing')"
            class="mt-4 w-full text-gray-600 hover:text-gray-900"
          >
            ← Back to Home
          </button>
        </div>
      </div>
    </div>

    <!-- Dashboard -->
    <div
      v-if="currentView === 'dashboard'"
      class="min-h-screen bg-linear-to-br from-blue-50 to-indigo-50"
    >
      <div class="max-w-[1440px] mx-auto px-6 py-8">
        <div class="flex justify-between items-center mb-8 flex-wrap gap-4">
          <h1 class="text-3xl font-bold text-gray-900">Dashboard</h1>
          <button
            @click="handleLogout"
            class="px-6 py-2 bg-red-500 text-white rounded-lg hover:bg-red-600 transition"
          >
            Logout
          </button>
        </div>

        <div class="grid sm:grid-cols-2 lg:grid-cols-4 gap-6 mb-8">
          <div v-for="(stat, i) in statsArray" :key="i" class="bg-white rounded-xl shadow-lg p-6">
            <div :class="['w-12 h-12 rounded-lg mb-4', stat.color]"></div>
            <p class="text-3xl font-bold text-gray-900">{{ stat.value }}</p>
            <p class="text-gray-600">{{ stat.label }}</p>
          </div>
        </div>

        <div class="bg-white rounded-xl shadow-lg p-6">
          <h2 class="text-xl font-bold text-gray-900 mb-4">Quick Actions</h2>
          <button
            @click="navigateTo('tickets')"
            class="px-6 py-3 bg-indigo-600 text-white rounded-lg hover:bg-indigo-700 transition"
          >
            Manage Tickets
          </button>
        </div>
      </div>
    </div>

    <!-- Ticket Management -->
    <div
      v-if="currentView === 'tickets'"
      class="min-h-screen bg-linear-to-br from-blue-50 to-indigo-50"
    >
      <div class="max-w-[1440px] mx-auto px-6 py-8">
        <div class="flex justify-between items-center mb-8 flex-wrap gap-4">
          <h1 class="text-3xl font-bold text-gray-900">Ticket Management</h1>
          <div class="flex gap-4">
            <button
              @click="navigateTo('dashboard')"
              class="px-6 py-2 bg-gray-500 text-white rounded-lg hover:bg-gray-600 transition"
            >
              Dashboard
            </button>
            <button
              @click="handleLogout"
              class="px-6 py-2 bg-red-500 text-white rounded-lg hover:bg-red-600 transition"
            >
              Logout
            </button>
          </div>
        </div>

        <button
          @click="toggleTicketForm"
          class="mb-6 px-6 py-3 bg-indigo-600 text-white rounded-lg hover:bg-indigo-700 transition"
        >
          {{ showTicketForm ? 'Cancel' : '+ Create New Ticket' }}
        </button>

        <Transition name="slide-fade">
          <div v-if="showTicketForm" class="bg-white rounded-xl shadow-lg p-6 mb-6">
            <h2 class="text-xl font-bold mb-4">
              {{ editingTicket ? 'Edit Ticket' : 'Create New Ticket' }}
            </h2>
            <div class="space-y-4">
              <div>
                <label class="block text-sm font-medium text-gray-700 mb-1">Title *</label>
                <input
                  v-model="ticketForm.title"
                  type="text"
                  class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 outline-none"
                />
                <p v-if="ticketErrors.title" class="text-red-500 text-sm mt-1">
                  {{ ticketErrors.title }}
                </p>
              </div>
              <div>
                <label class="block text-sm font-medium text-gray-700 mb-1">Description</label>
                <textarea
                  v-model="ticketForm.description"
                  class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 outline-none"
                  rows="3"
                />
              </div>
              <div class="grid md:grid-cols-2 gap-4">
                <div>
                  <label class="block text-sm font-medium text-gray-700 mb-1">Status *</label>
                  <select
                    v-model="ticketForm.status"
                    class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 outline-none"
                  >
                    <option value="open">Open</option>
                    <option value="in_progress">In Progress</option>
                    <option value="closed">Closed</option>
                  </select>
                </div>
                <div>
                  <label class="block text-sm font-medium text-gray-700 mb-1">Priority</label>
                  <select
                    v-model="ticketForm.priority"
                    class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 outline-none"
                  >
                    <option value="low">Low</option>
                    <option value="medium">Medium</option>
                    <option value="high">High</option>
                  </select>
                </div>
              </div>
              <button
                @click="handleTicketSubmit"
                class="px-6 py-2 bg-indigo-600 text-white rounded-lg hover:bg-indigo-700 transition"
              >
                {{ editingTicket ? 'Update Ticket' : 'Create Ticket' }}
              </button>
            </div>
          </div>
        </Transition>

        <div class="grid sm:grid-cols-2 lg:grid-cols-3 gap-6">
          <TransitionGroup name="list">
            <div
              v-for="ticket in tickets"
              :key="ticket.id"
              class="bg-white rounded-xl shadow-lg p-6"
            >
              <div class="flex justify-between items-start mb-3">
                <h3 class="text-lg font-bold text-gray-900 flex-1 mr-2">{{ ticket.title }}</h3>
                <span
                  :class="[
                    'px-3 py-1 rounded-full text-xs font-semibold whitespace-nowrap',
                    getStatusColor(ticket.status),
                  ]"
                >
                  {{ ticket.status.replace('_', ' ') }}
                </span>
              </div>
              <p v-if="ticket.description" class="text-gray-600 mb-4 text-sm">
                {{ ticket.description }}
              </p>
              <div class="flex gap-2">
                <button
                  @click="handleEditTicket(ticket)"
                  class="flex-1 px-4 py-2 bg-blue-500 text-white rounded-lg hover:bg-blue-600 transition text-sm"
                >
                  Edit
                </button>
                <button
                  v-if="ticket.id"
                  @click="handleDeleteTicket(ticket.id)"
                  class="flex-1 px-4 py-2 bg-red-500 text-white rounded-lg hover:bg-red-600 transition text-sm"
                >
                  Delete
                </button>
              </div>
            </div>
          </TransitionGroup>
        </div>

        <div v-if="tickets.length === 0" class="text-center py-12">
          <p class="text-gray-600 text-lg">No tickets yet. Create your first ticket!</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed, onMounted } from 'vue'

// Types
type View = 'landing' | 'login' | 'signup' | 'dashboard' | 'tickets'
type TicketStatus = 'open' | 'in_progress' | 'closed'
type TicketPriority = 'low' | 'medium' | 'high'
type ToastType = 'success' | 'error'
type TicketDraft = Omit<Ticket, 'id' | 'createdAt'>

interface User {
  email: string
  token: string
}

interface Ticket {
  id?: string
  title: string
  description?: string
  status: TicketStatus
  priority?: TicketPriority
  createdAt?: string
}

interface Toast {
  message: string
  type: ToastType
}

interface AuthForm {
  email: string
  password: string
}

interface ValidationErrors {
  [key: string]: string
}

interface Feature {
  title: string
  desc: string
}

interface Stat {
  label: string
  value: number
  color: string
}

// State
const currentView = ref<View>('landing')
const user = ref<User | null>(null)
const tickets = ref<Ticket[]>([])
const toast = ref<Toast | null>(null)

const authForm = ref<AuthForm>({ email: '', password: '' })
const authErrors = ref<ValidationErrors>({})

const ticketForm = ref<TicketDraft>({
  title: '',
  description: '',
  status: 'open',
  priority: 'medium',
})

const ticketErrors = ref<ValidationErrors>({})
const showTicketForm = ref(false)
const editingTicket = ref<Ticket | null>(null)

// Constants
const features: Feature[] = [
  { title: 'Create Tickets', desc: 'Easily create and track support tickets' },
  { title: 'Manage Status', desc: 'Update ticket status in real-time' },
  { title: 'Stay Organized', desc: 'Keep all your tickets in one place' },
]

// Computed
const stats = computed(() => ({
  total: tickets.value.length,
  open: tickets.value.filter((t) => t.status === 'open').length,
  inProgress: tickets.value.filter((t) => t.status === 'in_progress').length,
  closed: tickets.value.filter((t) => t.status === 'closed').length,
}))

const statsArray = computed<Stat[]>(() => [
  { label: 'Total Tickets', value: stats.value.total, color: 'bg-blue-500' },
  { label: 'Open', value: stats.value.open, color: 'bg-green-500' },
  { label: 'In Progress', value: stats.value.inProgress, color: 'bg-amber-500' },
  { label: 'Closed', value: stats.value.closed, color: 'bg-gray-500' },
])

// Lifecycle
onMounted(() => {
  const token = localStorage.getItem('ticketapp_session')
  if (token) {
    user.value = { email: 'user@example.com', token }
  }
  const savedTickets = localStorage.getItem('tickets')
  if (savedTickets) {
    tickets.value = JSON.parse(savedTickets)
  }
})

// Methods
const showToastMessage = (message: string, type: ToastType): void => {
  toast.value = { message, type }
  setTimeout(() => {
    toast.value = null
  }, 3000)
}

const navigateTo = (view: View): void => {
  if (['dashboard', 'tickets'].includes(view) && !user.value) {
    currentView.value = 'login'
    showToastMessage('Please log in to access this page', 'error')
    return
  }
  currentView.value = view
}

const validateAuth = (): boolean => {
  const errors: ValidationErrors = {}
  if (!authForm.value.email) errors.email = 'Email is required'
  else if (!/\S+@\S+\.\S+/.test(authForm.value.email)) errors.email = 'Email is invalid'
  if (!authForm.value.password) errors.password = 'Password is required'
  else if (authForm.value.password.length < 6)
    errors.password = 'Password must be at least 6 characters'
  authErrors.value = errors
  return Object.keys(errors).length === 0
}

const handleAuth = (): void => {
  if (!validateAuth()) return

  const token = btoa(`${authForm.value.email}:${Date.now()}`)
  localStorage.setItem('ticketapp_session', token)
  user.value = { email: authForm.value.email, token }
  showToastMessage(
    `${currentView.value === 'login' ? 'Logged in' : 'Signed up'} successfully!`,
    'success',
  )
  authForm.value = { email: '', password: '' }
  navigateTo('dashboard')
}

const handleLogout = (): void => {
  localStorage.removeItem('ticketapp_session')
  user.value = null
  currentView.value = 'landing'
  showToastMessage('Logged out successfully', 'success')
}

const validateTicket = (): boolean => {
  const errors: ValidationErrors = {}
  if (!ticketForm.value.title.trim()) errors.title = 'Title is required'
  if (!['open', 'in_progress', 'closed'].includes(ticketForm.value.status)) {
    errors.status = 'Invalid status'
  }
  ticketErrors.value = errors
  return Object.keys(errors).length === 0
}

const handleTicketSubmit = (): void => {
  if (!validateTicket()) return

  if (editingTicket.value) {
    const index = tickets.value.findIndex((t) => t.id === editingTicket.value!.id)
    tickets.value[index] = {
      ...tickets.value[index],
      ...ticketForm.value,
    }
  } else {
    const newTicket: Ticket = {
      ...ticketForm.value,
      id: Date.now().toString(),
      createdAt: new Date().toISOString(),
    }
    tickets.value.push(newTicket)
  }

  localStorage.setItem('tickets', JSON.stringify(tickets.value))
  showTicketForm.value = false
  editingTicket.value = null
  ticketForm.value = { title: '', description: '', status: 'open', priority: 'medium' }
}

const handleEditTicket = (ticket: Ticket): void => {
  editingTicket.value = ticket
  ticketForm.value = {
    title: ticket.title,
    description: ticket.description || '',
    status: ticket.status,
    priority: ticket.priority || 'medium',
  }
  showTicketForm.value = true
}

const handleDeleteTicket = (id: string): void => {
  if (confirm('Are you sure you want to delete this ticket?')) {
    tickets.value = tickets.value.filter((t) => t.id !== id)
    localStorage.setItem('tickets', JSON.stringify(tickets.value))
    showToastMessage('Ticket deleted successfully', 'success')
  }
}

const toggleTicketForm = (): void => {
  showTicketForm.value = !showTicketForm.value
  editingTicket.value = null
  ticketForm.value = { title: '', description: '', status: 'open', priority: 'medium' }
}

const getStatusColor = (status: TicketStatus): string => {
  const colors: Record<TicketStatus, string> = {
    open: 'bg-green-100 text-green-800',
    in_progress: 'bg-amber-100 text-amber-800',
    closed: 'bg-gray-100 text-gray-800',
  }
  return colors[status]
}
</script>

<style scoped>
.toast-enter-active,
.toast-leave-active {
  transition: all 0.3s ease;
}

.toast-enter-from,
.toast-leave-to {
  opacity: 0;
  transform: translateY(-20px);
}

.slide-fade-enter-active {
  transition: all 0.3s ease-out;
}

.slide-fade-leave-active {
  transition: all 0.2s cubic-bezier(1, 0.5, 0.8, 1);
}

.slide-fade-enter-from,
.slide-fade-leave-to {
  transform: translateY(-10px);
  opacity: 0;
}

.list-enter-active,
.list-leave-active {
  transition: all 0.3s ease;
}

.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: scale(0.9);
}
</style>
