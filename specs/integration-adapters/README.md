# EMR Integration Adapters

Danh sách EMR bên thứ 3 đã được tích hợp:

| EMR | Phiên bản | Status | Spec |
|-----|-----------|--------|------|
| Medpro HIS | v3.x | ✅ Done | medpro-adapter.yaml |
| Hsoft HIS | v2.x | 🚧 Building | hsoft-adapter.yaml |
| VNPT HIS | v1.x | 📋 Planned | - |
| Custom HIS | - | Per project | custom-template.yaml |

## Cách tích hợp EMR mới

BV cung cấp OpenAPI spec của EMR họ.
DEAI viết adapter để map data format.
Patient App không cần thay đổi gì.
