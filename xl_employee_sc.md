# XiLi

## interface_grpc

```bash
cd api/proto
python -m grpc_tools.protoc -I ./ --python_out=. --grpc_python_out=. biz/body_pose/v1/*.proto
python -m grpc_tools.protoc -I ./ --python_out=. --grpc_python_out=. biz/customer_flow/v1/*.proto
python -m grpc_tools.protoc -I ./ --python_out=. --grpc_python_out=. common/error/*.proto
python -m grpc_tools.protoc -I ./ --python_out=. --grpc_python_out=. common/graphics/*.proto
python -m grpc_tools.protoc -I ./ --python_out=. --grpc_python_out=. product/cus/xl_employee_sc/device/*.proto
python -m grpc_tools.protoc -I ./ --python_out=. --grpc_python_out=. product/cus/xl_employee_sc/platform/*.proto
```
