build: clean stackstorm.yaml

stackstorm.yaml: clean/stackstorm.yaml
	kustomize build clean > stackstorm.yaml

clean/stackstorm.yaml: values.yaml
	-helm repo add stackstorm https://helm.stackstorm.com/
	helm repo update
	helm template stackstorm stackstorm/stackstorm-ha --version 0.60.0 --namespace=stackstorm --values=values.yaml > $@

diff: stackstorm.yaml clean/stackstorm.yaml
	kustomize build . > diff.yaml
	diff stackstorm.yaml diff.yaml
	rm -f diff.yaml

.PHONY: clean
clean:
	rm -f clean/stackstorm.yaml
