# Migration `20200413222116-adding-count-fields`

This migration has been generated by Manuel Muñoz Solera at 4/13/2020, 10:21:16 PM.
You can check out the [state of the schema](./schema.prisma) after the migration.

## Database Steps

```sql
ALTER TABLE "public"."Capture" ADD COLUMN "diffindex" Decimal(65,30)   ;

ALTER TABLE "public"."Page" ADD COLUMN "endsAt" timestamp(3)   DEFAULT CURRENT_TIMESTAMP,
ADD COLUMN "reportcount" integer   ,
ADD COLUMN "startsAt" timestamp(3)   DEFAULT CURRENT_TIMESTAMP;

ALTER TABLE "public"."Report" ADD COLUMN "pagecount" integer   ;
```

## Changes

```diff
diff --git schema.prisma schema.prisma
migration 20200410210811-capture-unique-slug..20200413222116-adding-count-fields
--- datamodel.dml
+++ datamodel.dml
@@ -1,7 +1,7 @@
 datasource db {
   provider = "postgresql"
-  url = "***"
+  url      = env("POSTGRES_URL")
 }
 generator client {
   provider = "prisma-client-js"
@@ -12,19 +12,23 @@
   slug      String    @unique
   url       String?
   current   Boolean   @default(false)
   pages     Page[]    @relation(references: [id])
+  pagecount Int?
   captures  Capture[]
   createdAt DateTime  @default(now())
 }
 model Page {
-  id        String    @default(cuid()) @id
-  slug      String    @unique
-  url       String
-  captures  Capture[]
-  reports   Report[]  @relation(references: [id])
-  createdAt DateTime  @default(now())
+  id          String    @default(cuid()) @id
+  slug        String    @unique
+  url         String
+  captures    Capture[]
+  reports     Report[]  @relation(references: [id])
+  reportcount Int?
+  startsAt    DateTime? @default(now())
+  endsAt      DateTime? @default(now())
+  createdAt   DateTime  @default(now())
 }
 model Device {
   id        String    @default(cuid()) @id
@@ -41,8 +45,9 @@
   url       String?
   urlmin    String?
   urldiff   String?
   diff      Boolean  @default(false)
+  diffindex Float?
   page      Page     @relation(fields: [pageId], references: [id])
   pageId    String
   report    Report   @relation(fields: [reportId], references: [id])
   reportId  String
```

