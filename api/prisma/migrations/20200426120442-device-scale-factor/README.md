# Migration `20200426120442-device-scale-factor`

This migration has been generated by Manuel Muñoz Solera at 4/26/2020, 12:04:42 PM.
You can check out the [state of the schema](./schema.prisma) after the migration.

## Database Steps

```sql
ALTER TABLE "public"."Capture" DROP COLUMN "density",
ADD COLUMN "deviceScaleFactor" integer   ;

ALTER TABLE "public"."Device" DROP COLUMN "density",
ADD COLUMN "deviceScaleFactor" integer   ;
```

## Changes

```diff
diff --git schema.prisma schema.prisma
migration 20200426113922-adding-density..20200426120442-device-scale-factor
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
@@ -30,30 +30,30 @@
   createdAt   DateTime  @default(now())
 }
 model Device {
-  id        String    @default(cuid()) @id
-  slug      String    @unique
-  name      String
-  specs     String
-  captures  Capture[]
-  density   Int?
-  createdAt DateTime  @default(now())
+  id                String    @default(cuid()) @id
+  slug              String    @unique
+  name              String
+  specs             String
+  captures          Capture[]
+  deviceScaleFactor Int?
+  createdAt         DateTime  @default(now())
 }
 model Capture {
-  id        String   @default(cuid()) @id
-  slug      String   @unique
-  url       String?
-  urlmin    String?
-  urldiff   String?
-  diff      Boolean  @default(false)
-  diffindex Float?
-  density   Int?
-  page      Page     @relation(fields: [pageId], references: [id])
-  pageId    String
-  report    Report   @relation(fields: [reportId], references: [id])
-  reportId  String
-  device    Device   @relation(fields: [deviceId], references: [id])
-  deviceId  String
-  createdAt DateTime @default(now())
+  id                String   @default(cuid()) @id
+  slug              String   @unique
+  url               String?
+  urlmin            String?
+  urldiff           String?
+  diff              Boolean  @default(false)
+  diffindex         Float?
+  deviceScaleFactor Int?
+  page              Page     @relation(fields: [pageId], references: [id])
+  pageId            String
+  report            Report   @relation(fields: [reportId], references: [id])
+  reportId          String
+  device            Device   @relation(fields: [deviceId], references: [id])
+  deviceId          String
+  createdAt         DateTime @default(now())
 }
```


