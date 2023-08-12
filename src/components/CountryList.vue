<template>
    <div>
        <div class="mt-12 px-4 sm:px-6 lg:px-8">
            <div class="mt-8 flow-root">
                <div class="-mx-4 -my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
                    <div class="inline-block min-w-full py-2 align-middle sm:px-6 lg:px-8">
                        <form>
                            <label for="default-search"
                                class="mb-2 text-sm font-medium text-gray-900 sr-only dark:text-white">Search</label>
                            <div class="relative">
                                <div class="absolute inset-y-0 left-0 flex items-center pl-3 pointer-events-none">
                                    <svg class="w-4 h-4 text-gray-500 dark:text-gray-400" aria-hidden="true"
                                        xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 20 20">
                                        <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"
                                            stroke-width="2" d="m19 19-4-4m0-7A7 7 0 1 1 1 8a7 7 0 0 1 14 0Z" />
                                    </svg>
                                </div>
                                <input type="search" v-model="search"
                                    class="block w-full p-4 pl-10 text-sm text-gray-900 border border-gray-300 bg-gray-50 rounded-lg"
                                    placeholder="Search..." required>
                            </div>
                        </form>

                        <table class="min-w-full divide-y divide-gray-300">
                            <thead>
                                <tr>
                                    <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">
                                        Favorites
                                    </th>
                                    <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">
                                        Flag
                                    </th>
                                    <th scope="col"
                                        class="py-3.5 pl-4 pr-3 text-left text-sm font-semibold text-gray-900 sm:pl-0">
                                        Name
                                        <svg v-if="susun.name" @click="sortedArray('name')"
                                            xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
                                            stroke-width="1.5" stroke="currentColor"
                                            class="w-4 h-4 mt-1 ml-1 text-blue-500 hover:cursor-pointer hover:text-blue-600">
                                            <path stroke-linecap="round" stroke-linejoin="round"
                                                d="M19.5 13.5L12 21m0 0l-7.5-7.5M12 21V3" />
                                        </svg>
                                        <svg v-else @click="sortedArrayDesc('name')" xmlns="http://www.w3.org/2000/svg"
                                            fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"
                                            class="w-4 h-4 mt-1 ml-1 text-blue-500 hover:cursor-pointer hover:text-blue-600">
                                            <path stroke-linecap="round" stroke-linejoin="round"
                                                d="M8.25 6.75L12 3m0 0l3.75 3.75M12 3v18" />
                                        </svg>
                                    </th>
                                    <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">
                                        Capital City
                                        <svg v-if="susun.capital" @click="sortedArray('capital')"
                                            xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
                                            stroke-width="1.5" stroke="currentColor"
                                            class="w-4 h-4 mt-1 ml-1 text-blue-500 hover:cursor-pointer hover:text-blue-600">
                                            <path stroke-linecap="round" stroke-linejoin="round"
                                                d="M19.5 13.5L12 21m0 0l-7.5-7.5M12 21V3" />
                                        </svg>
                                        <svg v-else @click="sortedArrayDesc('capital')" xmlns="http://www.w3.org/2000/svg"
                                            fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"
                                            class="w-4 h-4 mt-1 ml-1 text-blue-500 hover:cursor-pointer hover:text-blue-600">
                                            <path stroke-linecap="round" stroke-linejoin="round"
                                                d="M8.25 6.75L12 3m0 0l3.75 3.75M12 3v18" />
                                        </svg>
                                    </th>
                                    <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">
                                        Region
                                        <svg v-if="susun.region" @click="sortedArray('region')"
                                            xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
                                            stroke-width="1.5" stroke="currentColor"
                                            class="w-4 h-4 mt-1 ml-1 text-blue-500 hover:cursor-pointer hover:text-blue-600">
                                            <path stroke-linecap="round" stroke-linejoin="round"
                                                d="M19.5 13.5L12 21m0 0l-7.5-7.5M12 21V3" />
                                        </svg>
                                        <svg v-else @click="sortedArrayDesc('region')" xmlns="http://www.w3.org/2000/svg"
                                            fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"
                                            class="w-4 h-4 mt-1 ml-1 text-blue-500 hover:cursor-pointer hover:text-blue-600">
                                            <path stroke-linecap="round" stroke-linejoin="round"
                                                d="M8.25 6.75L12 3m0 0l3.75 3.75M12 3v18" />
                                        </svg>
                                    </th>
                                    <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">
                                        Currency
                                    </th>
                                    <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">
                                        Language
                                    </th>
                                    <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">
                                        Population
                                    </th>
                                </tr>
                            </thead>
                            <tbody class="divide-y divide-gray-200">
                                <tr v-for="item in filteredCountries" :key="item.name">
                                    <td class="whitespace-nowrap py-4 pl-4 pr-3 text-sm font-medium text-gray-900 sm:pl-0">
                                        <input type="checkbox" v-model="item.isFavorite" @change="toggleFavorite(item)">
                                        <span v-if="item.isFavorite">❤️</span>
                                    </td>
                                    <td class="whitespace-nowrap px-3 py-4 text-4xl text-gray-500">
                                        {{ item.flag }}</td>
                                    <td class="whitespace-nowrap py-4 pl-4 pr-3 text-sm font-medium text-gray-900 sm:pl-0">
                                        <div v-html="getHighlightedText(item.name.common, search)"></div>
                                    </td>
                                    <td v-if="item.capital" class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                                        <div v-html="getHighlightedText(item.capital[0], search)"></div>
                                    </td>
                                    <td v-else class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                                        N/A
                                    </td>
                                    <td class="whitespace-nowrap py-4 pl-4 pr-3 text-sm font-medium text-gray-500 sm:pl-0">
                                        {{ item.region ? item.region : 'N/A' }}</td>
                                    <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                                        <li v-for="data in item.currencies" :key="data.name">
                                            {{ data.name }}
                                        </li>
                                    </td>
                                    <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                                        <li v-for="data in item.languages" :key="data.name">
                                            {{ data }}
                                        </li>
                                    </td>
                                    <td class="whitespace-nowrap py-4 pl-4 pr-3 bg-gray-50 text-sm font-medium text-gray-500 sm:pl-0">
                                        <div class="h-4 bg-green-500"
                                            :style="{ width: getPopulationPercentage(item.population) + '%' }">
                                        </div>
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import axios from 'axios';
export default {
    name: 'CountryList',
    data() {
        return {
            countries: [],
            susun: {
                'name': true,
                'region': true,
                'capital': true,
            },
            search: '',
        }
    },
    computed: {
        filteredCountries() {
            if (!this.search) {
                return this.countries;
            }
            const searchText = this.search.toLowerCase();
            return this.countries.filter(country => {
                return (
                    country.name.common.toLowerCase().includes(searchText) ||
                    (country.capital && country.capital[0].toLowerCase().includes(searchText))
                );
            });
        }
    },
    methods: {
        sortedArray(field) {
            if (field == 'name') {
                function compare(a, b) {
                    if (a.name.common < b.name.common)
                        return -1;
                    if (a.name.common > b.name.common)
                        return 1;
                    return 0;
                }
                this.susun.name = false
                return this.countries.sort(compare);
            } else if (field == 'region') {
                function compare(a, b) {
                    if (a[field] < b[field])
                        return -1;
                    if (a[field] > b[field])
                        return 1;
                    return 0;
                }
                this.susun.region = false
                return this.countries.sort(compare);
            } else if (field == 'capital') {
                function compare(a, b) {
                    if (a.capital && b.capital) {
                        if (a.capital[0] < b.capital[0]) {
                            return -1;
                        }
                        if (a.capital[0] > b.capital[0]) {
                            return 1;
                        }
                    }
                    return 0;
                }
                this.susun.capital = false
                return this.countries.sort(compare);
            }
        },
        sortedArrayDesc(field) {
            if (field == 'name') {
                function compare(a, b) {
                    if (a.name.common < b.name.common)
                        return 1;
                    if (a.name.common > b.name.common)
                        return -1;
                    return 0;
                }
                this.susun.name = true
                return this.countries.sort(compare);
            } else if (field == 'region') {
                function compare(a, b) {
                    if (a[field] < b[field])
                        return 1;
                    if (a[field] > b[field])
                        return -1;
                    return 0;
                }
                this.susun.region = true
                return this.countries.sort(compare);
            } else if (field == 'capital') {
                function compare(a, b) {
                    if (a.capital && b.capital) {
                        if (a.capital[0] < b.capital[0])
                            return 1;
                        if (a.capital[0] > b.capital[0])
                            return -1;
                        return 0;
                    }
                }
                this.susun.capital = true
                return this.countries.sort(compare);
            }
        },
        getHighlightedText(text, highlight) {
            const parts = text.split(new RegExp(`(${highlight})`, 'gi'));
            return parts.map((part) =>
                part.toLowerCase() === highlight.toLowerCase() ? `<span class="bg-yellow-200">${part}</span>` : part
            ).join('');
        },
        toggleFavorite(country) {
            const favorites = JSON.parse(localStorage.getItem('favorites') || '[]');
            const index = favorites.indexOf(country.name.common);
            console.log(country)
            if (index > -1) {
                favorites.splice(index, 1);
            } else {
                favorites.push(country.name.common);
            }

            localStorage.setItem('favorites', JSON.stringify(favorites));
            country.isFavorite = !country.isFavorite;
            window.location.reload()
        },
        getPopulationPercentage(population) {
            const maxPopulation = 1000000000;
            return (population / maxPopulation) * 100;
        },
    },
    mounted() {
        axios.get('https://restcountries.com/v3.1/all')
            .then(response => {
                this.countries = response.data.map(country => ({
                    ...country,
                    isFavorite: JSON.parse(localStorage.getItem('favorites') || '[]').includes(country.name.common)
                }));
            })
            .catch(error => {
                console.log(error)
            })
    }
}
</script>