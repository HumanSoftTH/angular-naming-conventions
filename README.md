# 📌 สรุปการตั้งชื่อ `id` ใน Angular + Ant Design สำหรับ Automated Testing

## ✅ 1. HTML Elements ที่ใช้ใน Angular
| Element      | Prefix     | ตัวอย่าง `id`            |
|-------------|-----------|-------------------------|
| `<button>`  | `btn`     | `btn-submit`           |
| `<input>`   | `input`   | `input-email`          |
| `<textarea>`| `textarea`| `textarea-message`     |
| `<select>`  | `select`  | `select-country`       |
| `<option>`  | `option`  | `option-thailand`      |
| `<checkbox>`| `checkbox`| `checkbox-remember-me` |
| `<radio>`   | `radio`   | `radio-gender-male`    |
| `<form>`    | `form`    | `form-login`           |
| `<table>`   | `tbl`     | `tbl-user-list`        |
| `<thead>`   | `thead`   | `thead-user`           |
| `<tbody>`   | `tbody`   | `tbody-user`           |
| `<tr>`      | `tr`      | `tr-user-1`            |
| `<td>`      | `td`      | `td-user-name`         |
| `<th>`      | `th`      | `th-user-email`        |
| `<div>`     | `div`     | `div-profile`          |
| `<span>`    | `span`    | `span-username`        |
| `<label>`   | `label`   | `label-password`       |
| `<a>`       | `link`    | `link-forgot-password` |
| `<img>`     | `img`     | `img-avatar`           |
| `<ul>`      | `ul`      | `ul-menu`              |
| `<li>`      | `li`      | `li-menu-item-1`       |
| `<modal>`   | `modal`   | `modal-confirm-delete` |
| `<tooltip>` | `tooltip` | `tooltip-info`         |

---

## ✅ 2. Ant Design Components

| Ant Design Component | Prefix     | ตัวอย่าง `id`                |
|----------------------|-----------|------------------------------|
| `<nz-button>`       | `btn`     | `btn-save`                   |
| `<nz-input>`        | `input`   | `input-username`             |
| `<nz-textarea>`     | `textarea`| `textarea-comment`           |
| `<nz-select>`       | `select`  | `select-role`                |
| `<nz-option>`       | `option`  | `option-admin`               |
| `<nz-checkbox>`     | `checkbox`| `checkbox-accept-terms`      |
| `<nz-radio>`        | `radio`   | `radio-male`                 |
| `<nz-form>`         | `form`    | `form-register`              |
| `<nz-table>`        | `tbl`     | `tbl-employee`               |
| `<nz-thead>`        | `thead`   | `thead-order`                |
| `<nz-tbody>`        | `tbody`   | `tbody-order`                |
| `<nz-tr>`           | `tr`      | `tr-order-1`                 |
| `<nz-td>`           | `td`      | `td-order-price`             |
| `<nz-th>`           | `th`      | `th-order-status`            |
| `<nz-modal>`        | `modal`   | `modal-edit-profile`         |
| `<nz-tooltip>`      | `tooltip` | `tooltip-help`               |
| `<nz-card>`         | `card`    | `card-user-info`             |
| `<nz-tabs>`         | `tabs`    | `tabs-dashboard`             |
| `<nz-tab>`         | `tab`     | `tab-overview`               |
| `<nz-tag>`         | `tag`     | `tag-status-active`          |
| `<nz-message>`     | `msg`     | `msg-success-save`           |
| `<nz-alert>`       | `alert`   | `alert-warning`              |
| `<nz-menu>`        | `menu`    | `menu-sidebar`               |
| `<nz-menu-item>`   | `menu-item` | `menu-item-dashboard`       |
| `<nz-dropdown>`    | `dropdown` | `dropdown-user-settings`    |

---

## 🎯 แนวทางการตั้งชื่อ `id`
1. ใช้ **Prefix ตามประเภทของ Element หรือ Component**
   - HTML: `btn-submit`, `input-email`, `tbl-user`
   - Ant Design: `btn-save`, `form-register`, `modal-confirm`
2. ใช้ **kebab-case** เช่น `btn-login`, `input-password`
3. อธิบายความหมายให้ **ชัดเจน**
4. ต้องไม่ซ้ำกันในแต่ละหน้า
5. หลีกเลี่ยงการใช้ `id` แบบ dynamic ที่เปลี่ยนแปลงได้

---

## ⚠️ คำแนะนำเพิ่มเติมเกี่ยวกับการตั้งชื่อ `id` ใน Angular + Ant Design

### 🎯 1. ระวัง `id` ซ้ำใน Component ที่เรียกใช้ Component อื่น

#### 🔹 ปัญหา:
เมื่อนำ Component หนึ่งไปใช้ซ้ำในหลายที่ หากกำหนด `id` ตายตัว อาจทำให้ `id` ซ้ำกัน ส่งผลให้ Automation Testing หรือลอจิกที่อ้างอิง `id` ทำงานผิดพลาด

#### ✅ วิธีแก้ไข:
1. ใช้ **`[attr.id]`** เพื่อกำหนด `id` แบบ dynamic
2. ใช้ **`@Input()`** ส่ง `id` จาก Parent Component

#### ❌ ตัวอย่างที่ผิด:
````html
// parent.component.html
<input id="input-user" [value]="user.name">
<child-component></child-component>

// child.component.html
<input id="input-user" [value]="user.name"> <!-- ❌ id ซ้ำ -->
````
#### ✅ ตัวอย่างที่ถูกต้อง:
````html
// parent.component.html
<input id="input-user" [value]="user.name">
<child-component></child-component>

// child.component.html
<input id="input-user-2" [value]="user.name"> <!-- ✅ id ไม่ซ้ำ -->
````
#### ✅ ตัวอย่างที่ถูกต้อง:
````html
// parent.component.html
<input id="input-user" [value]="user.name">
<child-component></child-component>

// child.component.html
<input [attr.id]="'input-user-' + uniqueId" [value]="user.name"> <!-- ✅ id ไม่ซ้ำ -->
````

### 🎯 2. ระวัง `id` ซ้ำเมื่อใช้ `ngFor` สร้างหลายๆ `input`

#### 🔹 ปัญหา:

การใช้ `ngFor` เพื่อสร้างหลายๆ `input` หรือ element ที่มี `id` ซ้ำกัน อาจทำให้การเข้าถึง element หรือการทดสอบอัตโนมัติผิดพลาด

#### ✅ วิธีแก้ไข:

1. ใช้ `[attr.id]` และเพิ่มค่าที่ไม่ซ้ำกัน เช่น `index`

#### ❌ ตัวอย่างที่ผิด:
````html
<div *ngFor="let user of users">
	<input id="input-user" [value]="user.name"> <!-- ❌ id ซ้ำ -->
</div>
````
#### ✅ ตัวอย่างที่ถูกต้อง:
````html
<div *ngFor="let user of users; let i = index">
	<input [attr.id]="'input-user-' + i" [value]="user.name"> <!-- ✅ id ไม่ซ้ำ -->
</div>
````
