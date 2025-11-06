<script></script>
<template>
    <div class="min-h-screen bg-gray-900 flex items-center justify-center p-4">
        <div class="max-w-md w-full p-12 bg-[#2a283b] flex flex-col justify-center rounded-xl shadow-2xl">
            <h2 class="text-white text-4xl font-semibold mb-8">Login here</h2>

            <form class="space-y-6">
                <div>
                    <input
                        type="text"
                        placeholder="Account"
                        class="w-full px-4 py-3 rounded-lg border-2 border-white focus:border-purple-500 focus:ring-1 focus:ring-purple-500 bg-transparent text-white placeholder-gray-400 transition"
                    />
                </div>

                <div>
                    <input
                        type="password"
                        placeholder="Enter your password"
                        class="w-full px-4 py-3 rounded-lg border-2 border-white focus:border-purple-500 focus:ring-1 focus:ring-purple-500 bg-transparent text-white placeholder-gray-400 transition"
                    />
                </div>

                <button type="submit" class="w-full py-3 bg-purple-600 hover:bg-purple-700 rounded-lg text-white font-semibold transition">
                    Create account
                </button>
            </form>

            <div class="mt-6 text-gray-400 text-sm">
                Already have an account?
                <a href="#" class="text-purple-400 hover:text-purple-300 transition font-medium">Log in</a>
            </div>
        </div>
    </div>
</template>
