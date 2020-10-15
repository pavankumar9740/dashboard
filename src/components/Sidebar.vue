<template>
    <div class="app-sidebar sidebar-shadow">
        <div class="app-header__logo">
            <div class="header__pane">
                <button type="button"
                        class="hamburger close-sidebar-btn hamburger--elastic"
                        v-bind:class="{ 'is-active' : isOpen }"
                        @click="toggleBodyClass('closed-sidebar')">
                    <span class="hamburger-box">
                        <span class="hamburger-inner"><img src="@/assets/images/icons/menu-back.png" alt=""></span>
                    </span>
                </button>
            </div>
        </div>
        <div class="app-sidebar-content sidebar-menu" @mouseover="toggleSidebarHover('add', 'open-sidebar')" @mouseleave="toggleSidebarHover('remove', 'open-sidebar')">
            <VuePerfectScrollbar class="app-sidebar-scroll" v-once>
                <aside>
                    <div class="nano">
                        <ul class="nano-content">
                            <li class="active">
                                <router-link to="/ViewDashboard">
                                    <span class="active-icon">
                                        <img src="@/assets/images/sidebar/dashboard.png" alt />
                                        <img src="@/assets/images/sidebar/dashboard-selected.png" alt />
                                    </span>
                                    <span class="sub-text">Dashboard</span>
                                </router-link>
                            </li>
                            <li v-if="isRouteAllowed('MfListing') || isRouteAllowed('SupplierManagement') || isRouteAllowed('MonthlyReturn')" class="sub-menu">
                                <b-dropdown ref="dropdown">
                                    <template v-slot:button-content>
                                        <a>
                                            <span class="active-icon">
                                                <img src="@/assets/images/sidebar/manufacturers.png" alt />
                                                <img src="@/assets/images/sidebar/manufacturers-selected.png" alt />
                                            </span>
                                            <span class="sub-text">Manufacturers</span>
                                            <i class="arrow down"></i>
                                        </a>
                                    </template>
                            <li v-if="isRouteAllowed('MfListing')">
                                <router-link to="/MfListing">Manufacturers</router-link>
                            </li>
                            <li v-if="isRouteAllowed('SupplierManagement')">
                                        <router-link to="/SupplierManagement">Suppliers</router-link>
                                    </li>
                                    <li v-if="isRouteAllowed('MonthlyReturn')">
                                        <router-link to="/MonthlyReturn"><span class="sub-text">Monthly Returns</span></router-link>
                                    </li>
                            </b-dropdown>
                            </li>
                            <li v-if="isRouteAllowed('Tpsaf')">
                                <router-link to="/tpsaf">
                                    <span class="active-icon">
                                        <img src="@/assets/images/sidebar/TPSAF.png" alt />
                                        <img src="@/assets/images/sidebar/TPSAF-selected.png" alt />
                                    </span>
                                    <span class="sub-text">TPSAF</span>
                                </router-link>
                            </li>
                            <li v-if="isRouteAllowed('DeliveryPartner')">
                                <router-link to="/DeliveryPartner">
                                    <span class="active-icon">
                                        <img src="@/assets/images/sidebar/package-explore.png" alt />
                                        <img src="@/assets/images/sidebar/package-explore-selected.png" alt />
                                    </span>
                                    <span class="sub-text">Delivery Partner</span>
                                </router-link>
                            </li>
                            <li class="sub-menu" v-if="isRouteAllowed('Order') || isRouteAllowed('MfOrders') || isRouteAllowed('ReturnOrder') || isRouteAllowed('StockOrders') ||  isRouteAllowed('InternalStockRequest') || isRouteAllowed('StockRequestList') || isRouteAllowed('ApproveRejectProduct') || isRouteAllowed('ChangeSKUProductName') || isRouteAllowed('ChangeSKUProductNamelisting')">
                                <b-dropdown ref="dropdown">
                                    <template v-slot:button-content>
                                        <a>
                                            <span class="active-icon">
                                                <img src="@/assets/images/sidebar/order.png" alt />
                                                <img src="@/assets/images/sidebar/order-selected.png" alt />
                                            </span>
                                            <span class="sub-text">Orders</span>
                                            <i class="arrow down"></i>
                                        </a>
                                    </template>
                            <li v-if="isRouteAllowed('PlaceOrder')">
                                <router-link to="/PlaceOrder">Place Order</router-link>
                            </li>
                            <li v-if="isRouteAllowed('Orders')">
                                <router-link to="/Orders">Orders List</router-link>
                            </li>
                            <li v-if="isRouteAllowed('ReturnOrder')">
                                <router-link to="/ReturnOrder">Order Returns </router-link>
                            </li>
                            <li v-if="isRouteAllowed('MfOrders')">
                                <!-- <router-link to="/Orders">Manufacturer Orders</router-link> -->
                                <router-link to="/MfOrders">Manufacturer Orders</router-link>
                            </li>
                            <li v-if="isRouteAllowed('StockOrders')">
                                <!-- <router-link to="/Orders">Stock Orders</router-link> -->
                                <router-link to="/StockOrders">Stock Orders</router-link>
                            </li>
                            <li v-if="isRouteAllowed('InternalStockRequest')">
                                <!-- <router-link to="/Orders">Stock Orders</router-link> -->
                                <router-link to="/InternalStockRequest">Internal Stock Transfer Request</router-link>
                            </li>
                            <li v-if="isRouteAllowed('StockRequestList')">
                                <!-- <router-link to="/Orders">Stock Orders</router-link> -->
                                <router-link to="/StockRequestList">Stock Requests</router-link>
                            </li>
                            <li v-if="isRouteAllowed('ApproveRejectProduct')">
                                <router-link to="/ChangeSkuProductApprove">ChangeSku / Product Approval</router-link>
                            </li>
                            <li v-if="isRouteAllowed('ChangeSKUProductName')">
                                <router-link to="/ChangeSKUProductName">Change SKU/Supplier</router-link>
                            </li>
                            <li v-if="isRouteAllowed('ChangeSKUProductNamelisting') || isRouteAllowed('ChangeSKUProductName')">
                                <router-link to="/ChangeSKUProductNamelisting">Change SKU/Supplier Listing</router-link>
                            </li>
                            </b-dropdown>
                            </li>
                            <li class="sub-menu" v-if="isRouteAllowed('PrintOrderPlacement') || isRouteAllowed('PrintOrders')">
                                <b-dropdown ref="dropdown">
                                    <template v-slot:button-content>
                                        <a>
                                            <span class="active-icon">
                                                <img src="@/assets/images/sidebar/Print-order.png" alt />
                                                <img src="@/assets/images/sidebar/Print-order-selected.png" alt />
                                            </span>
                                            <span class="sub-text">Print Order</span>
                                            <i class="arrow down"></i>
                                        </a>
                                    </template>
                            <li v-if="isRouteAllowed('PrintOrderPlacement')">
                                <router-link to="/PrintOrderPlacement">Place Print Order</router-link>
                            </li>
                            <li v-if="isRouteAllowed('PrintOrders')">
                                <router-link to="/PrintOrders">Print Orders</router-link>
                            </li>
                            </b-dropdown>
                            </li>
                            <li v-if="isRouteAllowed('MonthlyReturns')" class="sub-menu">
                                <a href="#">
                                    <span class="active-icon">
                                        <img src="@/assets/images/sidebar/manage-monthly-returns.png" alt />
                                        <img src="@/assets/images/sidebar/manage-monthly-returns-selected.png" alt />
                                    </span>
                                    <span class="sub-text">Manage Monthly Returns</span>
                                </a>
                            </li>
                            <li v-if="isRouteAllowed('ViewMf')" class="sub-menu">
                                <router-link :to="'/ViewMf/' + this.orgId">
                                    <span class="active-icon">
                                        <img src="@/assets/images/sidebar/registration-details.png" alt />
                                        <img src="@/assets/images/sidebar/registration-details-selected.png" alt />
                                    </span>
                                    <span class="sub-text">Registration Details</span>
                                </router-link>
                            </li>
                            <li v-if="isRouteAllowed('DailyConsumption')" class="sub-menu">
                                <a href="#">
                                    <span class="active-icon">
                                        <img src="@/assets/images/sidebar/daily-consumption.png" alt />
                                        <img src="@/assets/images/sidebar/daily-consumption-selected.png" alt />
                                    </span>
                                    <span class="sub-text">Daily Consumption</span>
                                </a>
                            </li>
                            <li v-if="isRouteAllowed('ProdMgmtHome') || isRouteAllowed('ReelSizeManagement') || isRouteAllowed('ProductManagement') ||isRouteAllowed('MeasurementUnits')" class="sub-menu">
                                <b-dropdown ref="dropdown">
                                    <template v-slot:button-content>
                                      <a>
                                            <span class="active-icon">
                                                <img src="@/assets/images/sidebar/user-management.png" alt />
                                                <img src="@/assets/images/sidebar/user-management-selected.png" alt />
                                            </span>
                                            <span class="sub-text">Configurations</span>
                                            <i class="arrow down"></i>
                                      </a>
                                    </template>
                            <li>
                                <router-link to="/ReelSizeManagement">Reel Size Management</router-link>
                            </li>
                            <li>
                                <router-link to="/MeasurementUnits">Measurement Units</router-link>
                            </li>
                            <li>
                                <router-link to="/ProductManagement">Product Management</router-link>
                            </li>
                            </b-dropdown>
                            </li>
                            <li v-if="isRouteAllowed('ConsumptionTpsaf')" class="sub-menu">
                                <b-dropdown ref="dropdown">
                                    <template v-slot:button-content>
                                        <a>
                                            <span class="active-icon">
                                                <img src="@/assets/images/sidebar/order.png" alt />
                                                <img src="@/assets/images/sidebar/order-selected.png" alt />
                                            </span>
                                            <span class="sub-text">Consumption</span>
                                            <i class="arrow down"></i>
                                        </a>
                                    </template>
                                    <ul>
                                        <li v-if="isRouteAllowed('ConsumptionTpsaf')"><router-link to="/tpsaf"><span class="sub-text">TPSAF</span></router-link></li>
                                    </ul>
                                </b-dropdown>
                            </li>
                            <li class="sub-menu">
                                <a href="#">
                                    <span class="active-icon">
                                        <img src="@/assets/images/sidebar/reports.png" alt />
                                        <img src="@/assets/images/sidebar/reports-selected.png" alt />
                                    </span>
                                    <span class="sub-text">Reports</span>
                                </a>
                            </li>
                            <li class="sub-menu" v-if="isRouteAllowed('UserManagement')">
                                <router-link to="/UserManagement">
                                    <span class="active-icon">
                                        <img src="@/assets/images/sidebar/user-management.png" alt />
                                        <img src="@/assets/images/sidebar/user-management-selected.png" alt />
                                    </span>
                                    <span class="sub-text">User Management</span>
                                </router-link>
                            </li>
                        </ul>
                    </div>
                </aside>
            </VuePerfectScrollbar>
        </div>
    </div>
</template>

<script>
    import VuePerfectScrollbar from 'vue-perfect-scrollbar';
    import jwt_decode from 'jwt-decode';
    import { getAllowedRoutes } from '../router/routeFunctions';

    export default {
        components: {
            VuePerfectScrollbar
        },
        data() {
            return {
                isOpen: false,
                orgId:0,
                sidebarActive: false,
                windowWidth: 0,
                allowedRoutes: []
            }
        },
        computed: {

        },
        created: function () {
            var token = process.env.NODE_ENV === "development" ? this.$root.user.access_token : this.$root.access_token;
            this.orgId =  this.role = jwt_decode(token).OrgId;
            this.role = jwt_decode(token).Role;
            this.allowedRoutes = getAllowedRoutes(this.role);
        },
        props: {
            sidebarbg: String,
        },
        methods: {

            toggleBodyClass(className) {
                const el = document.body;
                this.isOpen = !this.isOpen;

                if (this.isOpen) {
                    el.classList.add(className);
                } else {
                    el.classList.remove(className);
                }
            },
            toggleSidebarHover(add, className) {
                const el = document.body;
                this.sidebarActive = !this.sidebarActive;

                this.windowWidth = document.documentElement.clientWidth;

                if (this.windowWidth > '992') {
                    if (add === 'add') {
                        el.classList.add(className);
                    } else {
                        el.classList.remove(className);
                    }
                }
            },
            getWindowWidth() {
                this.windowWidth = document.documentElement.clientWidth;
            },
            isRouteAllowed(routeName) {
                return this.allowedRoutes.indexOf(routeName) != -1;
            }

        },
        mounted() {
            this.$nextTick(function () {
                window.addEventListener('resize', this.getWindowWidth);

                //Init
                this.getWindowWidth()
            });
			document.body.classList.remove('open-sidebar');
        },

        beforeDestroy() {
            window.removeEventListener('resize', this.getWindowWidth);
        }
    }
</script>
