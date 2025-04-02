##### Build
``` bash
docker build -t agentic_rag_app --no-cache .
```

##### Run
``` bash
docker run --env-file .env -p 8000:8000 -v $(pwd)/data:/app/data agentic_rag_app
```

##### Health Check
``` bash
curl -X GET "http://localhost:8000/health"
```

##### Recipe Query
``` bash
curl -X POST "http://localhost:8000/query" \
  -H "Content-Type: application/json" \
  -d '{"query": "best Thai curry recipe"}'
```

##### Kubernetes
``` bash
kubectl create pv thai-recipes-pv \
  --capacity=storage=1Gi \
  --access-modes=ReadWriteOnce \
  --host-path=/Users/lconnell/Development/thai-food-recipe-agentic-rag/data \
  --dry-run=client -o yaml > thai-recipes-pv.yaml
kubectl apply -f thai-recipes-pv.yaml
```