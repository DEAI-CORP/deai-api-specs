# DEAI API Specifications

OpenAPI 3.0 specs cho toàn bộ hệ sinh thái DEAI Corp.

## Services

| Service | Spec | Port | Status |
|---------|------|------|--------|
| CRM-web (Doctor/Nurse Portal) | [specs/openapi-crm-web.yaml](specs/openapi-crm-web.yaml) | 3000 | ✅ Ready |
| EMR | coming soon | 4000 | 🚧 Building |
| Patient App | coming soon | 3001 | 🚧 Building |
| LIS | coming soon | - | 📋 Planned |
| PACS | coming soon | - | 📋 Planned |
| Staff Portal | coming soon | - | 📋 Planned |

## Xem Interactive Docs

Paste URL sau vào [editor.swagger.io](https://editor.swagger.io):
```
https://raw.githubusercontent.com/DEAI-CORP/deai-api-specs/master/specs/openapi-crm-web.yaml
```

## Authentication — JWT RS256

Tất cả services dùng chung JWT RS256.  
Public key để verify token: [`keys/public.pem`](keys/public.pem)
```
Issuer:    crm-auth-service
Algorithm: RS256
Expiry:    15 minutes (access), 7 days (refresh)
```

### JWT Payload
```json
{
  "sub":           "user-uuid",
  "username":      "bsnguyenvana",
  "role":          "BS",
  "department_id": "dept-noi",
  "hospital_id":   "bv-001",
  "iss":           "crm-auth-service"
}
```

### Role Mapping
| CRM Role | Nghĩa | EMR Role |
|----------|-------|----------|
| BS | Bác sĩ | DOCTOR |
| DTT | Điều dưỡng trưởng | HEAD_NURSE |
| DV | Điều dưỡng viên | NURSE |
| DS | Dược sĩ | PHARMACIST |
| BGD | Ban giám đốc | ADMIN |
| TK | Thư ký | SECRETARY |
| LT | Lễ tân | RECEPTIONIST |
| KT/NS/MKT | Kế toán/Nhân sự/Marketing | ❌ NO_ACCESS |

## SSO Flow
```
1. Doctor click "Mở bệnh án EMR" trong CRM-web
2. CRM-web gọi POST /api/v1/auth/sso/emr-token
3. Nhận ssoToken (hết hạn 5 phút)
4. Redirect: window.open(`{EMR_URL}/sso?token={ssoToken}&visitId={visitId}`)
5. EMR verify token bằng public.pem → tự động đăng nhập
```
