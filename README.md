# k8s-proto
.proto files for k8s-api/istio-api - use for generate cue-schemas

inline TypeMeta go struct to proto for k8s-api & istio-api
```protobuf
message DestinationRule {
  optional string kind = 1; //inline
  optional string apiVersion = 2; //inline
  optional .k8s.io.apimachinery.pkg.apis.meta.v1.ObjectMeta metadata = 3;
  optional .istio.networking.v1alpha3.DestinationRule spec = 4;
  optional .istio.meta.v1alpha1.IstioStatus status = 5;
}
```

Use in you cue-module for generate definition

```bash
cd <root you cue-module>
# ls -la ->> see cue.mod
cue import proto ./k8s-proto/istio.io/client-go/pkg/apis/... \
    	--proto_path ./k8s-proto/istio.io/api \
    	--force
cue import proto ./k8s-proto/k8s.io/api/... \
        --force
```

---
 fyi any type generate field optional you may move `*_gen.cue` files to `cue.mod/pkg` 
and add constraint or create issue to this repo :3