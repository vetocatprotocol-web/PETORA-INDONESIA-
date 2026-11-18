# PETORA INDONESIA
# MASTER FULL-STACK PRODUCT & TECHNICAL SPECIFICATION

**Document ID:** PETORA-MASTER-SPEC-001  
**Version:** 1.0  
**Status:** Master Specification  
**Date:** 18 November 2026  
**Architecture:** Single Web Application  
**Frontend:** Next.js + Vercel  
**Backend:** Supabase  
**Database:** Supabase PostgreSQL  
**Development Model:** Autonomous Development  
**Specification Authority:** This document is the sole source of product and technical requirements for PETORA INDONESIA.

---

# 1. PROJECT OVERVIEW

## 1.1 Product Definition

PETORA INDONESIA adalah platform manajemen terintegrasi untuk mengelola operasional klinik hewan dan petshop dalam satu perusahaan dengan dukungan banyak cabang.

PETORA menggabungkan seluruh kegiatan operasional perusahaan ke dalam satu aplikasi web, meliputi:

1. Website informasi publik.
2. Sistem manajemen internal.
3. Portal pelanggan klinik.
4. Manajemen perusahaan dan cabang.
5. Manajemen pengguna dan karyawan.
6. Manajemen pelanggan dan hewan.
7. Operasional klinik hewan.
8. Manajemen farmasi dan obat.
9. Manajemen produk petshop.
10. Manajemen inventaris.
11. Manajemen pengadaan.
12. Point of Sale.
13. Manajemen kasir dan shift.
14. Manajemen keuangan.
15. Pelaporan dan audit.

Seluruh area aplikasi menggunakan satu codebase, satu sistem routing, satu halaman login, satu design system, satu integrasi backend, dan satu deployment aplikasi untuk setiap environment.

## 1.2 Business Objectives

- Mengintegrasikan operasional klinik dan petshop.
- Mendukung satu perusahaan dengan banyak cabang.
- Menyediakan pengelolaan hak akses secara dinamis.
- Memastikan keamanan data pelanggan dan rekam medis.
- Menjaga konsistensi transaksi dan persediaan.
- Mengurangi pekerjaan administratif manual.
- Menyediakan laporan bisnis yang dapat dipercaya.
- Memberikan pengalaman penggunaan yang konsisten.
- Memungkinkan pengembangan fitur secara bertahap.
- Menyediakan sistem yang siap digunakan dalam operasional nyata.

## 1.3 Architectural Principles

1. Single Web Application.
2. Single Company, Multi-Branch.
3. Modular Monolith.
4. Web First.
5. Environment-Based Domain.
6. Frontend Full Vercel.
7. Backend Full Supabase.
8. Single Login Experience.
9. Dynamic Role-Based Access Control.
10. Database-Level Security.
11. Transactional Business Logic.
12. Reusable Design System.
13. Auditable Operations.
14. No Fake Implementation.
15. Complete End-to-End Features.

---

# 2. APPLICATION ARCHITECTURE

## 2.1 Single Web Application

PETORA hanya memiliki satu aplikasi web.

Aplikasi mempunyai tiga area penggunaan:

| Area | Pengguna | Fungsi |
|---|---|---|
| Public Website | Pengunjung | Informasi perusahaan dan klinik |
| Internal Management | Karyawan dan manajemen | Seluruh operasional bisnis |
| Customer Portal | Pelanggan | Layanan mandiri pelanggan klinik |

Ketiga area bukan aplikasi terpisah.

Ketentuan:

- Satu Next.js application.
- Satu repository aplikasi.
- Satu codebase.
- Satu sistem routing.
- Satu halaman login.
- Satu halaman registrasi pelanggan.
- Satu design system.
- Satu sistem navigasi yang konsisten.
- Satu integrasi backend Supabase.
- Satu konfigurasi domain utama per environment.
- Satu deployment aplikasi per environment.

## 2.2 Public Website

Public Website dapat diakses tanpa login.

Fitur:

- Homepage.
- Profil perusahaan.
- Informasi cabang.
- Informasi layanan klinik.
- Informasi dokter.
- Informasi fasilitas.
- Jam operasional.
- Informasi kontak.
- Artikel dan edukasi.
- Informasi janji temu.
- Tombol masuk ke aplikasi.
- Navigasi menuju Customer Portal setelah login.

Konten publik harus berasal dari data yang memang diizinkan untuk dipublikasikan.

## 2.3 Internal Management

Area internal digunakan oleh seluruh karyawan dan manajemen.

Fitur:

- Dashboard berdasarkan role.
- Administrasi sistem.
- Organisasi dan cabang.
- User management.
- Role dan permission.
- Human resources.
- Customer management.
- Pet management.
- Clinic management.
- Appointment management.
- Queue management.
- Examination.
- Diagnosis.
- Treatment.
- EMR.
- Pharmacy.
- Vaccination.
- Hospitalization.
- Billing.
- Product management.
- Inventory.
- Procurement.
- POS.
- Cashier.
- Returns.
- Finance.
- Reporting.

## 2.4 Customer Portal

Customer Portal digunakan oleh pelanggan klinik.

Fitur:

- Dashboard pelanggan.
- Profil pelanggan.
- Profil hewan.
- Pengajuan janji temu.
- Status janji temu.
- Riwayat kunjungan.
- Rekam medis yang boleh dilihat pelanggan.
- Riwayat vaksinasi.
- Pengingat vaksinasi.
- Tagihan klinik.
- Status pembayaran.
- Notifikasi klinik.
- Pengaturan akun.

Pelanggan hanya dapat mengakses data yang menjadi haknya sendiri.

---

# 3. APPLICATION ROUTING

## 3.1 Routing Principles

Semua route harus berada dalam satu aplikasi.

- Public routes dapat diakses tanpa autentikasi.
- Protected routes memerlukan session.
- Internal routes hanya dapat digunakan oleh akun karyawan.
- Customer routes hanya dapat digunakan oleh akun pelanggan.
- Authorization harus dilakukan di server.
- Middleware digunakan sebagai lapisan navigasi dan proteksi awal, bukan satu-satunya pengaman.
- Setiap route harus mempunyai aturan akses yang terdokumentasi.

## 3.2 Public Routes

| Route | Fungsi |
|---|---|
| `/` | Homepage |
| `/about` | Profil perusahaan |
| `/branches` | Daftar cabang |
| `/branches/[branchId]` | Detail cabang |
| `/services` | Daftar layanan |
| `/services/[serviceId]` | Detail layanan |
| `/doctors` | Daftar dokter |
| `/doctors/[doctorId]` | Profil dokter |
| `/facilities` | Fasilitas klinik |
| `/articles` | Artikel edukasi |
| `/articles/[slug]` | Detail artikel |
| `/contact` | Informasi kontak |

## 3.3 Authentication Routes

| Route | Fungsi |
|---|---|
| `/login` | Satu halaman login seluruh jenis pengguna |
| `/register` | Registrasi pelanggan |
| `/forgot-password` | Pemulihan akses akun sesuai metode autentikasi |
| `/reset-password` | Pengaturan ulang credential jika didukung |
| `/auth/callback` | Authentication callback |
| `/logout` | Pengakhiran session |

Tidak boleh membuat halaman login terpisah untuk karyawan dan pelanggan.

## 3.4 Internal Routes

Semua halaman internal berada di bawah `/dashboard`.

| Route | Modul |
|---|---|
| `/dashboard` | Dashboard utama |
| `/dashboard/system` | System Administration |
| `/dashboard/organization` | Organization Management |
| `/dashboard/access` | User & Access Management |
| `/dashboard/hr` | Human Resource Management |
| `/dashboard/customers` | Customer Management |
| `/dashboard/pets` | Pet Management |
| `/dashboard/veterinary` | Veterinary Master Data |
| `/dashboard/appointments` | Appointment Management |
| `/dashboard/queues` | Queue Management |
| `/dashboard/examinations` | Examination Management |
| `/dashboard/diagnoses` | Diagnosis Management |
| `/dashboard/treatments` | Treatment Management |
| `/dashboard/medical-records` | EMR |
| `/dashboard/pharmacy` | Prescription & Pharmacy |
| `/dashboard/vaccinations` | Vaccination Management |
| `/dashboard/hospitalization` | Hospitalization Management |
| `/dashboard/billing` | Billing & Payment |
| `/dashboard/products` | Product Management |
| `/dashboard/inventory` | Inventory Management |
| `/dashboard/procurement` | Procurement Management |
| `/dashboard/pos` | POS & Sales |
| `/dashboard/cashier` | Cashier & Shift |
| `/dashboard/returns` | Returns & Refunds |
| `/dashboard/finance` | Finance Management |
| `/dashboard/reports` | Reporting & Audit |
| `/dashboard/notifications` | Internal Notification Center |
| `/dashboard/profile` | Profil karyawan |
| `/dashboard/settings` | Pengaturan akun |

Setiap modul mempunyai subroute untuk daftar, detail, tambah, ubah, dan tindakan lain sesuai kebutuhan.

Contoh:

- `/dashboard/customers`
- `/dashboard/customers/new`
- `/dashboard/customers/[customerId]`
- `/dashboard/customers/[customerId]/edit`

Pola yang sama digunakan pada modul lain.

## 3.5 Customer Portal Routes

Seluruh fitur pelanggan menggunakan prefix `/portal`.

| Route | Fungsi |
|---|---|
| `/portal` | Dashboard pelanggan |
| `/portal/profile` | Profil pelanggan |
| `/portal/profile/edit` | Ubah profil |
| `/portal/pets` | Daftar hewan |
| `/portal/pets/new` | Tambah hewan |
| `/portal/pets/[petId]` | Detail hewan |
| `/portal/pets/[petId]/edit` | Ubah data hewan |
| `/portal/appointments` | Daftar janji temu |
| `/portal/appointments/new` | Pengajuan janji temu |
| `/portal/appointments/[appointmentId]` | Detail janji temu |
| `/portal/appointments/[appointmentId]/edit` | Perubahan janji temu sesuai aturan |
| `/portal/visits` | Riwayat kunjungan |
| `/portal/visits/[visitId]` | Detail kunjungan |
| `/portal/medical-records` | Daftar rekam medis |
| `/portal/medical-records/[recordId]` | Detail rekam medis yang diizinkan |
| `/portal/vaccinations` | Riwayat vaksinasi |
| `/portal/vaccinations/[vaccinationId]` | Detail vaksinasi |
| `/portal/billing` | Daftar tagihan |
| `/portal/billing/[invoiceId]` | Detail tagihan |
| `/portal/notifications` | Notifikasi pelanggan |
| `/portal/settings` | Pengaturan akun |

Pelanggan tidak dapat mengakses halaman internal hanya dengan mengubah URL.

---

# 4. SINGLE LOGIN SYSTEM

## 4.1 Login Experience

PETORA menggunakan satu halaman login:

`/login`

Halaman tersebut digunakan oleh karyawan maupun pelanggan.

Tidak boleh terdapat:

- `/login/staff`
- `/login/customer`
- Halaman login karyawan terpisah.
- Halaman login pelanggan terpisah.
- Dua desain login yang berbeda.
- Dua sistem navigasi autentikasi yang tidak terintegrasi.

Satu halaman login harus memiliki desain yang konsisten dan mudah dipahami.

## 4.2 Login Flow

```text
                 OPEN /LOGIN
                      |
                      v
               ENTER CREDENTIALS
                      |
                      v
              SERVER AUTHENTICATION
                      |
                      v
             VALIDATE IDENTITY TYPE
                      |
              +-------+-------+
              |               |
              v               v
           STAFF           CUSTOMER
              |               |
              v               v
       VALIDATE STAFF     VALIDATE CUSTOMER
       PERMISSIONS        OWNERSHIP
              |               |
              v               v
        /DASHBOARD          /PORTAL
```

## 4.3 Staff Authentication

Metode login karyawan:

- Username.
- PIN tepat 6 digit.

Ketentuan:

- PIN hanya diverifikasi di server.
- PIN disimpan menggunakan hashing yang sesuai.
- Tidak menggunakan MFA.
- Rate limiting.
- Brute-force protection.
- Session expiration.
- Session revocation.
- Audit login.
- Secure cookie.
- Logout.

## 4.4 Customer Authentication

Pelanggan menggunakan halaman login yang sama dengan karyawan.

Customer identity harus dapat dibedakan secara tegas dari staff identity.

Credential pelanggan harus mengikuti kebijakan autentikasi pelanggan yang aman dan ditetapkan sebelum fitur autentikasi diimplementasikan.

Ketentuan:

- Tidak menggunakan staff account.
- Tidak mendapatkan role karyawan.
- Tidak dapat mengakses dashboard internal.
- Terhubung ke customer record yang benar.
- Satu identitas pelanggan tidak boleh dapat mengambil alih customer record lain.
- Session pelanggan harus dapat dicabut.
- Hak akses dibatasi pada data miliknya.

Metode credential pelanggan harus didokumentasikan sebagai keputusan teknis dan bisnis sebelum autentikasi pelanggan dibangun. Kesamaan halaman login tidak berarti harus memaksakan credential karyawan kepada pelanggan.

## 4.5 Login Form Behavior

Satu halaman login menyediakan:

- Input identitas akun.
- Input credential.
- Show/hide credential.
- Submit button.
- Loading state.
- Validation errors.
- Authentication errors.
- Account status feedback.
- Link registrasi pelanggan.
- Link pemulihan akses sesuai dukungan autentikasi.

Sistem menentukan jenis identitas di server berdasarkan akun yang berhasil diautentikasi.

Jangan menentukan jenis akun hanya berdasarkan input browser.

## 4.6 Post-Login Redirect

| Identity | Destination |
|---|---|
| Staff | `/dashboard` |
| Customer | `/portal` |

Jika pengguna memiliki tujuan awal sebelum login:

- Tujuan harus divalidasi.
- Staff hanya dapat diarahkan ke route internal yang diizinkan.
- Customer hanya dapat diarahkan ke route portal yang diizinkan.
- Public route tetap dapat diakses.
- Redirect eksternal yang tidak diizinkan harus ditolak.
- Pengguna yang sudah login tidak perlu kembali ke halaman login.

## 4.7 Session Isolation

- Staff session dan customer session harus dapat dibedakan.
- Staff session tidak memberikan akses Customer Portal secara otomatis.
- Customer session tidak memberikan akses internal.
- Authorization diperiksa di server pada setiap operasi.
- Session harus mempunyai masa berlaku dan mekanisme revocation.
- Logout harus mengakhiri session yang benar.
- Tidak boleh menggunakan identitas bersama untuk seluruh pengguna.

---

# 5. CUSTOMER REGISTRATION

## 5.1 Registration Route

`/register`

Halaman registrasi pelanggan merupakan bagian dari aplikasi yang sama.

Registrasi hanya untuk pelanggan.

Tidak tersedia registrasi mandiri untuk karyawan. Akun karyawan dibuat atau dikelola melalui User & Access Management oleh pengguna yang berwenang.

## 5.2 Registration Information

Informasi dasar:

- Nama lengkap.
- Identitas kontak yang diperlukan.
- Credential sesuai metode autentikasi pelanggan.
- Persetujuan kebijakan privasi.
- Persetujuan ketentuan layanan.

Data harus divalidasi di server.

## 5.3 Registration Workflow

```text
OPEN /REGISTER
      |
      v
FILL REGISTRATION FORM
      |
      v
SERVER VALIDATION
      |
      v
CREATE CUSTOMER IDENTITY
      |
      v
CREATE / LINK CUSTOMER PROFILE
      |
      v
ESTABLISH SESSION OR REQUEST VERIFICATION
      |
      v
REDIRECT TO /PORTAL
```

## 5.4 Customer Identity Mapping

Customer identity harus memiliki relasi yang jelas ke tabel customers.

Ketentuan:

- Identity ID tidak boleh diasumsikan sama dengan customer ID.
- Relasi harus menggunakan foreign key atau mapping yang tervalidasi.
- Satu identity hanya boleh terhubung dengan customer record yang sah.
- Proses linking akun ke customer lama harus diverifikasi.
- Registrasi tidak boleh otomatis mengambil alih data pelanggan berdasarkan nama saja.

---

# 6. TECHNOLOGY STACK

## 6.1 Frontend

| Technology | Responsibility |
|---|---|
| Next.js App Router | Application framework |
| React | UI |
| TypeScript | Type safety |
| Tailwind CSS | Styling |
| React Hook Form | Form management |
| Zod | Validation |
| TanStack Table | Data tables |
| TanStack Query | Server-state management bila diperlukan |
| Lucide | Icons |
| Chart Library | Analytics |
| Playwright | E2E tests |

## 6.2 Frontend Hosting

**Vercel**

- Next.js hosting.
- Build.
- Deployment.
- Preview.
- Environment variables.
- Domain configuration.
- HTTPS.
- Logs.
- Monitoring.
- Rollback.

## 6.3 Backend

**Supabase**

| Component | Responsibility |
|---|---|
| PostgreSQL | Database |
| Supabase Auth | Identity authentication |
| Edge Functions | Business APIs |
| Database Functions | Transactional operations |
| RLS | Data authorization |
| Storage | File storage |
| Migrations | Database versioning |
| Triggers | Database events |
| Realtime | Live updates where needed |

Tidak menggunakan NestJS atau Express sebagai backend utama.

## 6.4 Repository Tools

- GitHub.
- pnpm.
- ESLint.
- Prettier.
- Vitest.
- Playwright.
- Supabase CLI.
- GitHub Actions.

---

# 7. DOMAIN AND ENVIRONMENT

## 7.1 Domain Strategy

Domain mengikuti environment pengembangan.

| Environment | Example |
|---|---|
| Local | `http://localhost:3000` |
| Development | Configured development URL |
| Preview | Vercel preview URL |
| Staging | Configured staging URL |
| Production | Configured production domain |

Satu aplikasi dapat dijalankan melalui domain yang disediakan masing-masing environment.

Tidak mewajibkan subdomain terpisah.

## 7.2 Domain Requirements

- Domain tidak boleh hardcoded.
- Seluruh internal route menggunakan origin yang sama.
- Seluruh customer route menggunakan origin yang sama.
- Public route menggunakan origin yang sama.
- Callback URL mengikuti environment.
- Canonical URL mengikuti environment.
- Metadata mengikuti environment.
- Cookie policy mengikuti environment.
- Redirect mengikuti environment.
- Preview deployment harus dapat bekerja tanpa perubahan source code.

## 7.3 Environment Variables

```env
NODE_ENV=development
NEXT_PUBLIC_APP_URL=http://localhost:3000
NEXT_PUBLIC_APP_ENV=development

NEXT_PUBLIC_SUPABASE_URL=
NEXT_PUBLIC_SUPABASE_ANON_KEY=

SUPABASE_SERVICE_ROLE_KEY=
```

Service role key hanya tersedia di server.

Tidak boleh menyimpan secret dalam repository atau browser bundle.

---

# 8. REPOSITORY STRUCTURE

```text
petora/
├── AGENTS.md
├── README.md
├── package.json
├── pnpm-workspace.yaml
├── pnpm-lock.yaml
├── .env.example
├── .gitignore
│
├── apps/
│   └── web/
│       ├── AGENTS.md
│       ├── package.json
│       ├── next.config.ts
│       └── src/
│           ├── app/
│           │   ├── (public)/
│           │   ├── (auth)/
│           │   │   ├── login/
│           │   │   ├── register/
│           │   │   ├── forgot-password/
│           │   │   ├── reset-password/
│           │   │   └── auth/
│           │   ├── (internal)/
│           │   │   └── dashboard/
│           │   ├── (customer)/
│           │   │   └── portal/
│           │   ├── api/
│           │   ├── layout.tsx
│           │   ├── error.tsx
│           │   ├── global-error.tsx
│           │   ├── loading.tsx
│           │   └── not-found.tsx
│           │
│           ├── components/
│           │   ├── ui/
│           │   ├── forms/
│           │   ├── tables/
│           │   ├── navigation/
│           │   └── feedback/
│           │
│           ├── features/
│           │   ├── system/
│           │   ├── organization/
│           │   ├── access/
│           │   ├── hr/
│           │   ├── customers/
│           │   ├── pets/
│           │   ├── veterinary/
│           │   ├── appointments/
│           │   ├── queues/
│           │   ├── examinations/
│           │   ├── diagnosis/
│           │   ├── treatments/
│           │   ├── emr/
│           │   ├── pharmacy/
│           │   ├── vaccinations/
│           │   ├── hospitalization/
│           │   ├── billing/
│           │   ├── products/
│           │   ├── inventory/
│           │   ├── procurement/
│           │   ├── pos/
│           │   ├── cashier/
│           │   ├── returns/
│           │   ├── finance/
│           │   ├── reports/
│           │   └── customer-portal/
│           │
│           ├── lib/
│           │   ├── supabase/
│           │   ├── auth/
│           │   ├── authorization/
│           │   ├── env/
│           │   ├── validation/
│           │   ├── errors/
│           │   └── utils/
│           │
│           ├── hooks/
│           ├── types/
│           └── styles/
│
├── packages/
│   ├── shared/
│   ├── config/
│   └── ui/
│
├── supabase/
│   ├── AGENTS.md
│   ├── config.toml
│   ├── migrations/
│   ├── functions/
│   ├── tests/
│   └── seed.sql
│
├── docs/
│   ├── architecture/
│   ├── database/
│   ├── security/
│   ├── workflows/
│   ├── testing/
│   └── decisions/
│
└── scripts/
```

---

# 9. FRONTEND SPECIFICATION

## 9.1 Design Direction

| Property | Specification |
|---|---|
| Visual | Clinical |
| Theme | Light |
| Typography | System |
| Responsive | Desktop, tablet, mobile |
| Migration | Gradual |
| Component Strategy | Reusable Design System |
| Accessibility | WCAG-oriented |

## 9.2 Layout System

### Public Layout

- Header.
- Main navigation.
- Hero.
- Content.
- Footer.
- Mobile navigation.

### Authentication Layout

- PETORA brand.
- Login form.
- Registration form.
- Authentication feedback.
- Recovery links.
- Responsive layout.

Login dan registrasi menggunakan design system yang sama.

### Internal Layout

- Sidebar.
- Topbar.
- Breadcrumb.
- Branch selector.
- Notification center.
- User menu.
- Dashboard content.

### Customer Layout

- Customer navigation.
- Profile menu.
- Pet selector.
- Notification center.
- Customer workspace.

## 9.3 Reusable UI Components

- Button.
- Input.
- Password/PIN Input.
- Textarea.
- Select.
- Combobox.
- Checkbox.
- Radio.
- Date Picker.
- Time Picker.
- Dialog.
- Drawer.
- Modal.
- Dropdown.
- Tooltip.
- Tabs.
- Badge.
- Alert.
- Toast.
- Data Table.
- Pagination.
- Search.
- Filter.
- File Upload.
- Form Field.
- Form Error.
- Empty State.
- Loading State.
- Error State.
- Confirmation Dialog.
- Page Header.
- Breadcrumb.
- Stat Card.
- Chart Container.

## 9.4 Form Standards

Semua form wajib memiliki:

- Client-side validation.
- Server-side validation.
- Field-level errors.
- Form-level errors.
- Loading state.
- Duplicate submission prevention.
- Success feedback.
- Error feedback.
- Accessible labels.
- Unsaved changes handling jika diperlukan.

## 9.5 Table Standards

- Pagination.
- Sorting.
- Search.
- Filtering.
- Responsive behavior.
- Empty state.
- Loading state.
- Error state.
- Permission-aware actions.

---

# 10. BACKEND SPECIFICATION

## 10.1 Backend Responsibilities

### Next.js Server Layer

- Server Components.
- Route Handlers.
- Server Actions bila sesuai.
- Session-aware data access.
- Request validation.
- Secure redirects.
- Server-side authorization.

### Supabase Edge Functions

- Business APIs.
- Server-side business operations.
- Authorization checks.
- Multi-table orchestration.
- Input validation.
- Integrasi eksternal jika dibutuhkan.

### PostgreSQL Functions

- Transactional operations.
- Stock movements.
- Checkout.
- Payment allocation.
- Financial posting.
- Business invariants.

### PostgreSQL

- Persistence.
- Constraints.
- RLS.
- Indexes.
- Transactions.
- Audit records.

## 10.2 Backend Contract

Setiap operasi harus mempunyai:

- Operation name.
- Purpose.
- Request schema.
- Response schema.
- Authentication requirement.
- Permission requirement.
- Branch scope.
- Validation rules.
- Error codes.
- Audit requirements.
- Transaction requirements.
- Test scenarios.

## 10.3 API Response

Success:

```json
{
  "success": true,
  "data": {},
  "meta": {}
}
```

Error:

```json
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Data tidak valid",
    "details": {}
  }
}
```

---

# 11. DATABASE SPECIFICATION

## 11.1 Database Standards

- Supabase PostgreSQL.
- UUID identifiers.
- Foreign keys.
- Unique constraints.
- Check constraints.
- Indexes.
- RLS.
- Versioned migrations.
- Transactional functions.
- Audit trail.
- Branch-aware data model.
- Timezone-aware timestamps.
- Numeric data types for monetary values.

## 11.2 Database Domains

### Company & Organization

- companies
- branches
- departments
- positions
- employees
- employee_assignments
- work_schedules

### Identity & Authorization

- user_profiles
- staff_accounts
- customer_accounts
- roles
- permissions
- role_permissions
- user_roles
- user_branch_access
- sessions
- authentication_events

### Customer & Pets

- customers
- customer_addresses
- customer_notes
- pets
- pet_species
- pet_breeds
- pet_ownerships
- pet_weights
- pet_medical_alerts

### Clinic

- clinic_services
- clinic_rooms
- doctors
- appointments
- queues
- examinations
- examination_vitals
- diagnoses
- treatments
- medical_records
- prescriptions
- prescription_items
- vaccinations
- hospitalizations
- hospitalization_monitoring

### Billing & Payments

- invoices
- invoice_items
- payments
- payment_allocations
- refunds
- billing_adjustments

### Products & Inventory

- product_categories
- products
- product_units
- product_prices
- stock_locations
- inventory_balances
- inventory_movements
- stock_adjustments
- stock_transfers
- stock_counts

### Procurement

- suppliers
- purchase_requests
- purchase_orders
- purchase_order_items
- goods_receipts
- goods_receipt_items

### POS & Cashier

- sales
- sale_items
- cashier_shifts
- cashier_shift_transactions
- cash_movements
- receipts
- sales_returns

### Finance & Reporting

- finance_accounts
- financial_transactions
- expenses
- reconciliations
- report_snapshots jika diperlukan

### System & Audit

- system_settings
- audit_logs
- approval_requests
- approval_actions
- notifications
- file_metadata

### Customer Portal

- customer_notification_preferences
- customer identity mapping
- customer-visible medical record projection jika diperlukan

Daftar ini adalah database domain. Struktur final wajib mempunyai ERD dan data dictionary yang lengkap.

## 11.3 Identity Mapping

Identity dan business entity harus dipisahkan.

- Staff identity terhubung ke staff account.
- Customer identity terhubung ke customer account.
- Customer account terhubung ke customer record.
- Jangan mengasumsikan Auth user ID sama dengan customer ID.
- Relasi harus menggunakan foreign key atau mapping tervalidasi.
- Linking akun pelanggan lama wajib mempunyai verifikasi kepemilikan.
- Tidak boleh menghubungkan akun berdasarkan nama saja.

## 11.4 Multi-Branch Data Model

- Satu perusahaan.
- Banyak cabang.
- Data operasional memiliki company dan branch relationship sesuai kebutuhan.
- User dapat memiliki akses ke beberapa cabang.
- Branch context diverifikasi di server.
- Tidak mempercayai branch ID dari browser.
- Akses lintas cabang memerlukan permission.
- Transfer stok mencatat sumber dan tujuan.

## 11.5 Data Integrity

- Foreign keys.
- Unique constraints.
- Check constraints.
- Transactional operations.
- Audit history.
- Explicit lifecycle states.
- Soft delete hanya jika sesuai.
- Financial data integrity.
- Inventory movement integrity.
- Medical record history preservation.

---

# 12. AUTHORIZATION & ROLE MANAGEMENT

## 12.1 Dynamic RBAC

Role dan permission dikelola secara dinamis.

Contoh permission:

```text
customers.view
customers.create
customers.update

pets.view
pets.create
pets.update

appointments.view
appointments.create
appointments.approve
appointments.cancel

medical_records.view
medical_records.create
medical_records.update

inventory.view
inventory.adjust
inventory.transfer

finance.view
finance.reconcile

cashier.shift.open
cashier.shift.close
```

## 12.2 Roles

1. Super Admin.
2. Owner.
3. Management.
4. Branch Manager.
5. Receptionist.
6. Veterinarian.
7. Veterinary Assistant.
8. Pharmacy Staff.
9. Cashier.
10. Inventory Staff.
11. Procurement Staff.
12. Finance.
13. HR.

Super Admin mengelola administrasi sistem, role, dan permission. Super Admin tidak otomatis mendapatkan kewenangan persetujuan bisnis Owner.

## 12.3 Authorization Requirements

- Default deny.
- Least privilege.
- Server-side permission validation.
- Database RLS.
- Branch scope enforcement.
- Customer ownership enforcement.
- Field-level data authorization.
- Sensitive action audit.
- No client-trusted authorization.

## 12.4 Customer Isolation

Customer hanya dapat melihat:

- Profil sendiri.
- Hewan miliknya.
- Appointment miliknya.
- Riwayat kunjungan yang diizinkan.
- Rekam medis yang dipublikasikan untuk pelanggan.
- Riwayat vaksinasi hewannya.
- Tagihan miliknya.
- Notifikasi miliknya.

Customer tidak dapat melihat:

- Data customer lain.
- Internal doctor notes.
- Internal staff notes.
- Harga modal.
- Data stok internal.
- Data karyawan.
- Konfigurasi sistem.
- Internal financial reports.

---

# 13. BUSINESS MODULES

PETORA mempunyai 25 modul utama.

## A. System & Organization

### 1. System Administration

- System settings.
- Global configuration.
- Company configuration.
- Audit logs.
- Approval settings.
- System monitoring.

### 2. Organization Management

- Company profile.
- Branch management.
- Department management.
- Position management.
- Branch settings.

### 3. User & Access Management

- Staff accounts.
- Username and PIN.
- Role management.
- Permission management.
- Branch access.
- Session management.

### 4. Human Resource Management

- Employee profiles.
- Employee assignments.
- Doctor profiles.
- Work schedules.
- Employment status.

## B. Customer & Clinic

### 5. Customer Management

- Customer profiles.
- Addresses.
- Notes.
- Customer history.
- Search.

### 6. Pet Management

- Pet profiles.
- Species.
- Breeds.
- Ownership.
- Weight history.
- Medical alerts.

### 7. Veterinary Master Data

- Clinic services.
- Doctors.
- Rooms.
- Schedules.
- Service pricing.

### 8. Appointment Management

- Appointment requests.
- Scheduling.
- Confirmation.
- Rescheduling.
- Cancellation.
- Status tracking.

### 9. Queue Management

- Queue numbering.
- Queue status.
- Calling.
- Monitoring.

### 10. Examination Management

- Examination forms.
- Vital signs.
- Observations.
- Examination results.

### 11. Diagnosis Management

- Diagnosis catalog.
- Clinical findings.
- Diagnosis history.
- Classification.

### 12. Treatment Management

- Treatment planning.
- Medical actions.
- Treatment execution.
- Follow-up.

### 13. Electronic Medical Record

- Medical history.
- Clinical notes.
- Examination records.
- Attachments.
- Access control.

### 14. Prescription & Pharmacy

- Prescription creation.
- Prescription items.
- Dispensing.
- Medicine history.
- Inventory linkage.

### 15. Vaccination Management

- Vaccination records.
- Vaccine catalog.
- Vaccination schedule.
- Next due date.
- Reminders.

### 16. Hospitalization Management

- Admission.
- Room assignment.
- Monitoring.
- Treatment.
- Discharge.

### 17. Billing & Payment

- Invoice generation.
- Invoice items.
- Payments.
- Payment allocation.
- Refunds.
- Billing history.

## C. Petshop & Transactions

### 18. Product Management

- Product catalog.
- Categories.
- SKU.
- Units.
- Selling prices.

### 19. Inventory Management

- Stock balances.
- Stock movements.
- Adjustments.
- Transfers.
- Stock counts.

### 20. Procurement Management

- Suppliers.
- Purchase requests.
- Purchase orders.
- Goods receipt.
- Procurement history.

### 21. POS & Sales Management

- Sales transactions.
- Product selection.
- Checkout.
- Payment.
- Receipt.
- Sales history.

### 22. Cashier & Shift Management

- Shift opening.
- Cash in/out.
- Cashier transactions.
- Reconciliation.
- Shift closing.

Setiap kasir memiliki shift sendiri-sendiri.

### 23. Returns & Refunds

- Return requests.
- Return items.
- Return approval.
- Refund.
- Inventory adjustment.
- Return history.

## D. Finance & Control

### 24. Finance Management

- Income.
- Expenses.
- Financial transactions.
- Reconciliation.
- Financial summaries.

### 25. Reporting & Audit

- Operational reports.
- Sales reports.
- Financial reports.
- Inventory reports.
- Employee activity reports.
- Audit reports.

---

# 14. CROSS-MODULE FEATURES

1. Authentication.
2. Dynamic RBAC.
3. Multi-Branch.
4. Audit Trail.
5. Notification Center.
6. File Management.
7. Global Search.
8. Dashboard Analytics.
9. Approval Workflow.
10. Import & Export.
11. System Configuration.
12. Backup & Recovery.

Setiap fitur bersama wajib mempunyai kontrak, permission, audit policy, dan integration tests.

---

# 15. BUSINESS RULES

Keputusan bisnis yang harus diterapkan:

| Rule | Value |
|---|---|
| DEC-001 Tax | `config_exclusive` |
| DEC-002 Return Approval | `owner_threshold` |
| Discount Policy | `owner_only` |
| Transaction Rounding | `rupiah` |
| Service Pricing | `variable` |
| Payment Methods | `multi` |
| Stock at Checkout | `block` |
| DEC-006 Cashier Shifts | Setiap kasir memiliki shift sendiri-sendiri |

## 15.1 Tax

- Menggunakan `config_exclusive`.
- Perhitungan mengikuti konfigurasi pajak.
- Perubahan konfigurasi tercatat dalam audit.

## 15.2 Return Approval

- Menggunakan `owner_threshold`.
- Persetujuan mengikuti threshold Owner.
- Approval tidak boleh dilewati.

## 15.3 Discount

- Menggunakan `owner_only`.
- Diskon mempunyai pemberi persetujuan.
- Nilai dan alasan diskon dicatat.

## 15.4 Rounding

- Menggunakan `rupiah`.
- Pembulatan konsisten pada semua transaksi.
- Perhitungan dapat diaudit.

## 15.5 Service Pricing

- Menggunakan `variable`.
- Harga aktual disimpan dalam transaksi.
- Master price tidak mengubah transaksi historis.

## 15.6 Payment

- Mendukung metode pembayaran `multi`.
- Mendukung payment allocation.
- Status pembayaran dihitung dari transaksi valid.

## 15.7 Inventory at Checkout

- Checkout diblokir jika stok tidak cukup.
- Validasi stok di backend/database.
- Pengurangan stok atomik.
- Concurrent checkout diuji untuk mencegah overselling.

## 15.8 Cashier Shift

- Setiap kasir memiliki shift sendiri.
- Shift mencatat waktu buka dan tutup.
- Transaksi terhubung dengan shift.
- Cash movements dicatat.
- Rekonsiliasi dapat dilakukan.

---

# 16. BUSINESS WORKFLOWS

## 16.1 Customer Registration

Registration → Identity Creation → Customer Mapping → Session → Customer Portal.

## 16.2 Login

Login → Server Authentication → Identity Resolution → Authorization → Role-Based Redirect.

## 16.3 Clinic Appointment

Appointment Request → Validation → Confirmation → Queue → Examination.

## 16.4 Clinic Visit

Examination → Diagnosis → Treatment → EMR → Billing → Payment.

## 16.5 Prescription

Prescription → Medicine Availability → Dispensing → Inventory Movement.

## 16.6 Vaccination

Schedule → Administration → Record → Next Due Date → Reminder.

## 16.7 Hospitalization

Admission → Room Assignment → Monitoring → Treatment → Billing → Discharge.

## 16.8 Petshop Sales

Product Selection → Stock Validation → Checkout → Payment → Inventory Deduction → Receipt.

## 16.9 Procurement

Purchase Request → Approval → Purchase Order → Goods Receipt → Inventory Update.

## 16.10 Cashier

Open Shift → Transactions → Cash Movements → Reconciliation → Close Shift.

## 16.11 Returns

Return Request → Owner Threshold Validation → Approval → Refund → Inventory Adjustment.

Setiap workflow harus mempunyai state definitions, allowed transitions, permission, audit, failure handling, dan automated tests.

---

# 17. SECURITY SPECIFICATION

## 17.1 Application Security

- HttpOnly cookies.
- Secure cookies on HTTPS.
- SameSite policy.
- CSRF protection.
- Input validation.
- Output encoding.
- Rate limiting.
- Brute-force protection.
- Security headers.
- Secret management.
- Error sanitization.
- Session expiration.
- Session revocation.

## 17.2 Database Security

- RLS untuk semua tabel yang memerlukan proteksi.
- Default deny.
- Policy berdasarkan identity dan authorization context.
- Tidak mengandalkan frontend filtering.
- Service role key hanya di server.
- Function privileges dibatasi.
- SECURITY DEFINER direview.
- Cross-customer access tests.
- Cross-branch access tests.

## 17.3 Audit Trail

Catat:

- Login/logout.
- Perubahan role.
- Perubahan permission.
- Perubahan customer.
- Perubahan EMR.
- Transaksi.
- Pembayaran.
- Refund.
- Stock adjustment.
- Approval.
- Konfigurasi.

Audit memuat actor, timestamp, action, resource, dan informasi perubahan yang diperlukan.

---

# 18. STORAGE AND FILE MANAGEMENT

Supabase Storage digunakan untuk:

- Foto hewan.
- Dokumen pelanggan.
- Lampiran medis.
- Dokumen karyawan.
- Dokumen procurement.
- Lampiran transaksi.
- Public website assets.

Ketentuan:

- Private bucket untuk file sensitif.
- Public bucket hanya untuk aset publik.
- Signed URL untuk private files.
- Storage policies.
- MIME type validation.
- File size limits.
- File metadata.
- Tidak ada URL publik permanen untuk file sensitif.

---

# 19. NOTIFICATION SYSTEM

Notification Center mendukung:

- Appointment updates.
- Queue notifications.
- Vaccination reminders.
- Billing notifications.
- Payment status.
- Procurement updates.
- Approval requests.
- System notifications.

Setiap notifikasi mempunyai:

- Recipient.
- Type.
- Title.
- Content.
- Related resource.
- Read status.
- Created timestamp.

Notifikasi internal dan pelanggan harus memiliki batas akses terpisah.

---

# 20. REPORTING & ANALYTICS

Dashboard menyesuaikan role dan branch scope.

### Owner

- Ringkasan perusahaan.
- Pendapatan.
- Performa cabang.
- Penjualan.
- Operasional.
- Approval.

### Branch Manager

- Kinerja cabang.
- Kunjungan.
- Penjualan.
- Stok.
- Shift.
- Aktivitas karyawan.

### Veterinarian

- Jadwal praktik.
- Janji temu.
- Antrean.
- Pemeriksaan.
- Follow-up.

### Cashier

- Shift aktif.
- Transaksi.
- Kas masuk/keluar.
- Rekonsiliasi.

### Inventory Staff

- Stok.
- Stock movements.
- Stock transfers.
- Stock counts.

Seluruh laporan harus mengikuti permission dan branch scope.

---

# 21. TESTING & QUALITY ASSURANCE

## 21.1 Unit Testing

- Business rules.
- Validation.
- Permission evaluation.
- Pricing.
- Tax.
- Rounding.
- Stock.
- State transitions.

## 21.2 Integration Testing

- Edge Functions.
- Database Functions.
- PostgreSQL transactions.
- RLS.
- Authentication.
- Storage policies.
- Cross-module operations.

## 21.3 End-to-End Testing

Minimal test scenarios:

1. Public homepage.
2. Single login page.
3. Staff authentication.
4. Customer authentication.
5. Staff redirect.
6. Customer redirect.
7. Customer registration.
8. Staff route protection.
9. Customer route protection.
10. Role-based dashboard.
11. Branch access.
12. Customer data isolation.
13. Pet registration.
14. Appointment.
15. Queue.
16. Examination.
17. EMR.
18. Prescription.
19. Vaccination.
20. Billing.
21. Payment.
22. Inventory.
23. Procurement.
24. POS.
25. Cashier shift.
26. Return approval.
27. Finance.
28. Reporting.

## 21.4 Quality Gates

Setiap perubahan harus melewati:

- Lint.
- Typecheck.
- Unit tests.
- Integration tests.
- E2E tests yang relevan.
- Build.
- Security checks.
- Migration checks.
- Regression checks.

Tidak boleh menyatakan fitur selesai jika hanya frontend tersedia.

---

# 22. PERFORMANCE & RELIABILITY

## Performance

- Server rendering sesuai kebutuhan.
- Pagination.
- Database indexing.
- Query optimization.
- Appropriate caching.
- Avoid N+1 queries.
- Avoid fetching entire datasets.

## Reliability

- Consistent error handling.
- Transactional consistency.
- Idempotency.
- Safe retry.
- Backup.
- Recovery.
- Monitoring.

## Accessibility

- Semantic HTML.
- Keyboard navigation.
- Accessible labels.
- Focus management.
- Color contrast.
- Screen reader support.

## Maintainability

- Modular code.
- Reusable components.
- Typed contracts.
- Automated tests.
- Documentation.
- Consistent naming.
- Dependency management.

---

# 23. DEPLOYMENT & ENVIRONMENT MANAGEMENT

## 23.1 Platforms

| Component | Platform |
|---|---|
| Web Application | Vercel |
| Database | Supabase |
| Authentication | Supabase |
| Backend Functions | Supabase Edge Functions |
| Database Logic | PostgreSQL |
| Storage | Supabase Storage |
| Source Control | GitHub |
| CI | GitHub Actions |

## 23.2 Environment Mapping

| Environment | Frontend | Backend |
|---|---|---|
| Local | Next.js local | Supabase local |
| Development | Vercel development bila digunakan | Supabase development |
| Preview | Vercel preview | Environment Supabase yang ditentukan |
| Staging | Vercel staging | Supabase staging |
| Production | Vercel production | Supabase production |

## 23.3 Deployment Rules

- Frontend melalui Vercel.
- Backend melalui Supabase.
- Migration versioned.
- Preview tidak sembarangan menggunakan production data.
- Secret dipisahkan per environment.
- Production migrations harus direview.
- Backup dan recovery diuji.
- Domain mengikuti environment.
- Remote deployment dan production database changes memerlukan persetujuan yang sesuai.

## 23.4 CI/CD

```text
Git Push
   |
   v
Install Dependencies
   |
   v
Lint
   |
   v
Typecheck
   |
   v
Unit Tests
   |
   v
Integration Tests
   |
   v
Build
   |
   v
Security Checks
   |
   v
Migration Checks
   |
   v
Deployment Approval
   |
   v
Vercel Deployment
```

---

# 24. DOCUMENTATION STRUCTURE

```text
docs/
├── architecture/
│   ├── system-architecture.md
│   ├── application-routing.md
│   ├── authentication-flow.md
│   └── environment-configuration.md
│
├── database/
│   ├── erd.md
│   ├── data-dictionary.md
│   └── migration-guide.md
│
├── security/
│   ├── authentication.md
│   ├── authorization.md
│   ├── permission-matrix.md
│   └── rls-policies.md
│
├── workflows/
│   ├── clinic-workflows.md
│   ├── inventory-workflows.md
│   ├── financial-workflows.md
│   └── approval-workflows.md
│
├── testing/
│   ├── test-strategy.md
│   └── test-scenarios.md
│
└── decisions/
    └── decision-register.md
```

Semua dokumentasi harus sesuai dengan implementasi aktual.

---

# 25. DEVELOPMENT PHASES

## Phase 0 — Foundation

- Repository audit.
- AGENTS.md.
- pnpm monorepo.
- Next.js foundation.
- Supabase local initialization.
- Environment configuration.
- Documentation.
- Design system foundation.
- Single login UI foundation.
- Public homepage.
- CI foundation.

## Phase 1 — Core Platform & Authentication

- Database foundation.
- Identity model.
- Staff authentication.
- Customer authentication.
- Single login flow.
- Customer registration.
- Identity mapping.
- Session management.
- Organization.
- Branches.
- Users.
- Roles.
- Permissions.
- RLS.
- Audit.

## Phase 2 — Customer & Pet

- Customer management.
- Pet management.
- Ownership.
- Medical alerts.
- Customer history.

## Phase 3 — Clinic Master Data

- Clinic services.
- Doctors.
- Rooms.
- Schedules.
- Service pricing.

## Phase 4 — Clinic Operations

- Appointments.
- Queues.
- Examinations.
- Diagnosis.
- Treatments.
- EMR.

## Phase 5 — Medical Services

- Prescriptions.
- Pharmacy.
- Vaccinations.
- Hospitalization.

## Phase 6 — Billing & Payments

- Invoices.
- Invoice items.
- Payments.
- Payment allocation.
- Refunds.

## Phase 7 — Product & Inventory

- Products.
- Categories.
- Inventory balances.
- Stock movements.
- Adjustments.
- Transfers.
- Stock counts.

## Phase 8 — Procurement

- Suppliers.
- Purchase requests.
- Purchase orders.
- Goods receipts.

## Phase 9 — POS & Cashier

- POS.
- Sales.
- Cashier shifts.
- Cash movements.
- Reconciliation.

## Phase 10 — Finance & Reporting

- Finance.
- Expenses.
- Reconciliation.
- Reports.
- Analytics.

## Phase 11 — Public Website & Customer Portal

- Public content management.
- Branch information.
- Service information.
- Customer profile.
- Pet profiles.
- Appointment requests.
- Customer-visible medical records.
- Vaccination history.
- Billing.
- Notifications.

## Phase 12 — Integration & Release

- Full regression.
- Security review.
- Performance review.
- Operational validation.
- Backup and recovery validation.
- Production readiness.

Setiap fase memiliki acceptance criteria dan approval gate. Penyelesaian satu fase harus dibuktikan melalui hasil pengujian.

---

# 26. DEFINITION OF DONE

Modul hanya boleh dinyatakan COMPLETE jika:

1. Database schema tersedia.
2. Migration tersedia.
3. RLS diterapkan.
4. Backend business logic berfungsi.
5. Server-side validation berfungsi.
6. Authorization diuji.
7. Branch scope diuji.
8. Frontend terintegrasi dengan backend.
9. Semua form berfungsi.
10. Semua tabel berfungsi.
11. Loading, error, empty, dan success states tersedia.
12. Audit diterapkan jika relevan.
13. Unit tests lulus.
14. Integration tests lulus.
15. E2E tests relevan lulus.
16. Tidak ada fake buttons.
17. Tidak ada placeholder atau stub yang dinyatakan selesai.
18. Tidak ada hardcoded business data yang seharusnya berasal dari database.
19. Dokumentasi diperbarui.
20. Build dan CI lulus.

Status pekerjaan:

- NOT STARTED.
- IN PROGRESS.
- BLOCKED.
- INCOMPLETE.
- COMPLETE.

Status COMPLETE hanya boleh diberikan jika tersedia bukti implementasi dan pengujian.

---

# 27. FINAL SYSTEM CONFIGURATION

| Category | Specification |
|---|---|
| Product | PETORA INDONESIA |
| Application | Single Web Application |
| Codebase | Single Next.js application |
| Application Areas | Public, Internal, Customer |
| Login | One shared login page |
| Login Route | `/login` |
| Customer Registration | `/register` |
| Staff Destination | `/dashboard` |
| Customer Destination | `/portal` |
| Internal Route Prefix | `/dashboard` |
| Customer Route Prefix | `/portal` |
| Frontend | Next.js + React + TypeScript |
| Hosting | Vercel |
| Backend | Supabase |
| Database | Supabase PostgreSQL |
| Business API | Supabase Edge Functions |
| Transaction Logic | PostgreSQL Functions |
| Authentication | Supabase-based secure identity |
| Authorization | Dynamic RBAC + RLS |
| Storage | Supabase Storage |
| Company Model | Single Company |
| Branch Model | Multi-Branch |
| Platform | Web First |
| Domain | Environment-Based |
| Staff Credential | Username + 6-digit PIN |
| MFA | Not used |
| Visual Direction | Clinical |
| Theme | Light |
| Typography | System |
| Responsive | Desktop, Tablet, Mobile |
| Business Modules | 25 |
| Source Control | GitHub |
| Package Manager | pnpm |

---

# 28. AUTHORITATIVE DEVELOPMENT INSTRUCTIONS

Dokumen ini merupakan satu-satunya sumber informasi produk dan teknis PETORA INDONESIA bagi autonomous developer.

Autonomous developer wajib:

1. Mengikuti seluruh spesifikasi di dokumen ini.
2. Menggunakan satu aplikasi Next.js.
3. Menyatukan Public Website, Internal Management, dan Customer Portal.
4. Menggunakan satu halaman login `/login`.
5. Menggunakan satu halaman registrasi pelanggan `/register`.
6. Memisahkan identity staff dan customer secara aman.
7. Mengarahkan staff ke `/dashboard`.
8. Mengarahkan customer ke `/portal`.
9. Menyediakan seluruh route Customer Portal.
10. Tidak membuat login terpisah untuk staff dan customer.
11. Tidak membuat deployment terpisah berdasarkan area aplikasi.
12. Tidak mengunci domain pada nama tertentu.
13. Mengikuti environment configuration.
14. Menggunakan Vercel untuk frontend.
15. Menggunakan Supabase untuk backend dan database.
16. Menegakkan business logic di server/database.
17. Menegakkan authorization melalui server dan RLS.
18. Tidak membuat fake buttons.
19. Tidak membuat placeholder atau stub yang dianggap selesai.
20. Tidak mengubah keputusan bisnis yang telah disetujui.
21. Tidak mengubah keputusan yang masih PENDING tanpa persetujuan.
22. Tidak mengklaim pengujian lulus tanpa menjalankannya.
23. Tidak mengklaim deployment berhasil tanpa bukti.
24. Memperbarui dokumentasi dan pengujian setiap perubahan.
25. Mengikuti phase gate dan acceptance criteria.

## FINAL DIRECTIVE

Bangun PETORA INDONESIA sebagai satu aplikasi web terintegrasi dengan satu halaman login yang digunakan oleh karyawan dan pelanggan, satu sistem routing, satu codebase, dan satu domain utama yang mengikuti environment.

Pengguna harus diarahkan ke area yang tepat berdasarkan identity dan authorization yang telah diverifikasi oleh server.

Seluruh 25 modul bisnis harus mempunyai frontend, backend, database, keamanan, business logic, dan pengujian yang terintegrasi.

Jangan menyatakan pekerjaan selesai tanpa bukti implementasi dan hasil pengujian yang dapat diverifikasi.
