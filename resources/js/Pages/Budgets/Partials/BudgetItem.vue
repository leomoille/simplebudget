<script setup>
import {EllipsisVerticalIcon, PlusIcon} from '@heroicons/vue/20/solid';
import {Menu, MenuButton, MenuItem, MenuItems} from '@headlessui/vue';

const statuses = {
    'Mis à jour': 'text-green-700 bg-green-50 ring-green-600/20',
    'In progress': 'text-gray-600 bg-gray-50 ring-gray-500/10',
    Archivé: 'text-yellow-800 bg-yellow-50 ring-yellow-600/20',
};
const projects = [
    {
        id: 1,
        name: 'Mon budget perso',
        href: '#',
        // status: 'Complete',
        createdBy: 'Leslie Alexander',
        dueDate: 'March 17, 2023',
        dueDateTime: '2023-03-17T00:00Z',
    },
    {
        id: 2,
        name: 'Voyage au Canada',
        href: '#',
        status: 'Mis à jour',
        createdBy: 'Leslie Alexander',
        dueDate: 'May 5, 2023',
        dueDateTime: '2023-05-05T00:00Z',
    },
    {
        id: 3,
        name: 'Budget pour la fac',
        href: '#',
        status: 'Archivé',
        createdBy: 'Courtney Henry',
        dueDate: 'June 10, 2023',
        dueDateTime: '2023-06-10T00:00Z',
    },
];
</script>

<template>
    <div v-if="false">
        <div class="text-center">
            <svg
                class="mx-auto h-12 w-12 text-gray-400" fill="none" viewBox="0 0 24 24" stroke="currentColor"
                aria-hidden="true">
                <path
                    vector-effect="non-scaling-stroke" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                    d="M9 13h6m-3-3v6m-9 1V7a2 2 0 012-2h6l2 2h6a2 2 0 012 2v8a2 2 0 01-2 2H5a2 2 0 01-2-2z" />
            </svg>
            <h3 class="mt-2 text-sm font-semibold text-gray-900">Aucun budget</h3>
            <p class="mt-1 text-sm text-gray-500">Commencez dès maintenant en créant un budget.</p>
            <div class="mt-6">
                <button
                    type="button"
                    class="inline-flex items-center rounded-md bg-indigo-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">
                    <PlusIcon class="-ml-0.5 mr-1.5 h-5 w-5" aria-hidden="true" />
                    Nouveau budget
                </button>
            </div>
        </div>
    </div>
    <div v-else>
        <ul role="list" class="divide-y divide-gray-100">
            <li v-for="project in projects" :key="project.id" class="flex items-center justify-between gap-x-6 py-5">
                <div class="min-w-0">
                    <div class="flex items-start gap-x-3">
                        <p class="text-sm/6 font-semibold text-gray-900">
                            {{ project.name }}
                        </p>
                        <div v-if="project.status">
                            <p :class="[statuses[project.status], 'mt-0.5 whitespace-nowrap rounded-md px-1.5 py-0.5 text-xs font-medium ring-1 ring-inset']">
                                {{ project.status }}
                            </p>
                        </div>
                    </div>
                    <div class="mt-1 flex items-center gap-x-2 text-xs/5 text-gray-500">
                        <p class="whitespace-nowrap">
                            Dernière mise à jour
                            <time :datetime="project.dueDateTime">{{ project.dueDate }}</time>
                        </p>
                        <svg viewBox="0 0 2 2" class="h-0.5 w-0.5 fill-current">
                            <circle cx="1" cy="1" r="1" />
                        </svg>
                        <p class="truncate">Créé par {{ project.createdBy }}</p>
                    </div>
                </div>
                <div class="flex flex-none items-center gap-x-4">
                    <a
                        :href="project.href"
                        class="hidden rounded-md bg-white px-2.5 py-1.5 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50 sm:block"
                    >Voir le budget<span class="sr-only">, {{ project.name }}</span>
                    </a>
                    <Menu as="div" class="relative">
                        <MenuButton class="-m-2.5 block p-2.5 text-gray-500 hover:text-gray-900">
                            <span class="sr-only">Open options</span>
                            <EllipsisVerticalIcon class="h-5 w-5" aria-hidden="true" />
                        </MenuButton>
                        <transition
                            enter-active-class="transition ease-out duration-100"
                            enter-from-class="transform opacity-0 scale-95"
                            enter-to-class="transform opacity-100 scale-100"
                            leave-active-class="transition ease-in duration-75"
                            leave-from-class="transform opacity-100 scale-100"
                            leave-to-class="transform opacity-0 scale-95">
                            <MenuItems
                                class="absolute right-0 z-10 mt-2 w-32 origin-top-right rounded-md bg-white py-2 shadow-lg ring-1 ring-gray-900/5 focus:outline-none">
                                <MenuItem v-slot="{ active }">
                                    <a
                                        href="#"
                                        :class="[active ? 'bg-gray-50 outline-none' : '', 'block px-3 py-1 text-sm/6 text-gray-900']"
                                    >Edit<span class="sr-only">, {{ project.name }}</span></a
                                    >
                                </MenuItem>
                                <MenuItem v-slot="{ active }">
                                    <a
                                        href="#"
                                        :class="[active ? 'bg-gray-50 outline-none' : '', 'block px-3 py-1 text-sm/6 text-gray-900']"
                                    >Move<span class="sr-only">, {{ project.name }}</span></a
                                    >
                                </MenuItem>
                                <MenuItem v-slot="{ active }">
                                    <a
                                        href="#"
                                        :class="[active ? 'bg-gray-50 outline-none' : '', 'block px-3 py-1 text-sm/6 text-gray-900']"
                                    >Delete<span class="sr-only">, {{ project.name }}</span></a
                                    >
                                </MenuItem>
                            </MenuItems>
                        </transition>
                    </Menu>
                </div>
            </li>
        </ul>
    </div>
</template>
