<script></script>
<template>
    <div class="min-h-screen flex items-center justify-center p-4 bg-cover bg-center" style="background-image: url('/public/chef.webp')">
        <div class="max-w-sm w-full p-12 flex flex-col justify-center bg-white/40 backdrop-blur-[20px] rounded-xl shadow-2xl border border-white/40">
            <h2 class="text-black text-3xl font-semibold mb-8">Sign Up</h2>

            <form class="space-y-6">
                <div>
                    <input
                        type="text"
                        placeholder="Account"
                        class="w-full px-4 py-3 rounded-lg border border-white/50 text-white placeholder-gray-300 transition focus:border-black focus:ring-2 focus:ring-black focus:ring-opacity-50 focus:outline-none bg-black/30"
                    />
                </div>
                <div>
                    <input
                        type="password"
                        placeholder="Enter your password"
                        class="space-y-1 w-full px-4 py-3 rounded-lg border border-white/50 text-white placeholder-gray-300 transition focus:border-black focus:ring-2 focus:ring-black focus:ring-opacity-50 focus:outline-none bg-black/30"
                    />
                </div>
                <div>
                    <button type="submit" class="w-full py-3 bg-black rounded-lg text-white font-semibold transition">Create account</button>
                </div>
            </form>

            <div class="mt-6 text-black text-sm text-center">
                <span class="mr-5">Already have an account ?</span>
                <button class="px-3 py-0.5 rounded-full transition inline-flex items-center text-sm hover:bg-white">
                    <a href="#" class="font-bold text-black">Log in</a>
                </button>
            </div>
        </div>
    </div>
</template>
