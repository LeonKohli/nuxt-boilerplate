<script setup lang="ts">
import type { NuxtError } from '#app'

const props = defineProps({
  error: Object as () => NuxtError
})

const router = useRouter()
const handleError = () => clearError({ redirect: '/' })

// Error status code constants
const ERROR_CODES = {
  NOT_FOUND: 404,
  FORBIDDEN: 403,
  SERVER_ERROR: 500
} as const

// Error messages mapping
const ERROR_MESSAGES = {
  [ERROR_CODES.NOT_FOUND]: {
    title: 'Page not found',
    message: "Sorry, the page you're looking for doesn't exist."
  },
  [ERROR_CODES.FORBIDDEN]: {
    title: 'Access denied',
    message: "You don't have permission to access this resource."
  },
  [ERROR_CODES.SERVER_ERROR]: {
    title: 'Server error',
    message: 'Something went wrong on our end. Please try again later.'
  },
  default: {
    title: 'An error occurred',
    message: 'Something unexpected happened. Please try again.'
  }
} as const

const errorConfig = computed(() => {
  const statusCode = props.error?.statusCode
  return ERROR_MESSAGES[statusCode as keyof typeof ERROR_MESSAGES] || ERROR_MESSAGES.default
})

const errorTitle = computed(() => errorConfig.value.title)

const errorMessage = computed(() => props.error?.statusMessage || errorConfig.value.message)
</script>

<template>
    <div class="min-h-screen flex items-center justify-center px-4 py-16">
      <div class="w-full max-w-md space-y-8 text-center">
        <!-- Error status code -->
        <div class="space-y-2">
          <h1 class="text-7xl font-bold tracking-tighter text-muted-foreground/20">
            {{ error?.statusCode || '500' }}
          </h1>
          <h2 class="text-3xl font-bold tracking-tight">
            {{ errorTitle }}
          </h2>
        </div>

        <!-- Error message -->
        <p class="text-muted-foreground text-lg">
          {{ errorMessage }}
        </p>

        <!-- Action buttons -->
        <div class="flex flex-col sm:flex-row gap-4 justify-center pt-4">
          <Button
            @click="handleError"
            size="lg"
            class="min-w-[140px]"
          >
            <Icon name="lucide:home" class="mr-2 h-4 w-4" />
            Go home
          </Button>
          <Button
            @click="router.back()"
            variant="outline"
            size="lg"
            class="min-w-[140px]"
          >
            <Icon name="lucide:arrow-left" class="mr-2 h-4 w-4" />
            Go back
          </Button>
        </div>
      </div>
    </div>

</template>