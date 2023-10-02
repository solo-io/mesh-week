# Mesh Week

A week of Istio goodness (with focus for the exam).

CNCF announced a new certification called Istio Certified Associate (ICA). Join [Peter Jausovec](https://twitter.com/pjausovec), [Marino Wijay](https://twitter.com/virtualized6ix), and [Alessandro Vozza](https://twitter.com/bongo), three Istio, Cilium, Kubernetes, and overall cloud-native experts, for a series of live streams called Mesh Week.

Each live stream will be about 1 hour and will focus on a different topic from the [Istio Certified associate exam curriculum](https://training.linuxfoundation.org/certification/istio-certified-associate-ica/). We’ll explain the concepts, talk about them, and see them in practice with hands-on demos. There will also be plenty of opportunities to ask questions.

These sessions are for anyone interested in Istio and preparing for the Istio Certified Associate exam. All you need to participate is a computer with Kind installed. Basic knowledge of Kubernetes and Docker is required.

## Schedule

- [Session 1: Istio installation, upgrade & configuration](#session-1-istio-installation-upgrade--configuration)
- [Session 2: Traffic management](#session-2-traffic-management)
- [Session 3: Resiliency and fault injection](#session-3-resiliency-and-fault-injection)
- [Session 4: Securing workloads](#session-4-securing-workloads)
- [Session 5: Advanced scenarios](#session-5-advanced-scenarios)

# Session 1: Istio installation, upgrade & configuration

[Watch the recording](https://www.youtube.com/watch?v=w_8Gg_jsAbU)

To start Mesh Week, we’ll go through the Istio installation topic. You’ll learn about Istio installation profiles, how to install Istio using Istio CLI (`istioctl`), how to customize the installation using the Istio Operator API, and how to install Istio using Helm charts.

Areas of focus from the Istio Certified Associate exam curriculum:

- Using the Istio CLI to install a basic cluster
- Customizing the Istio installation with the IstioOperator API
- Using overlays to manage Istio component settings

## Tips

- Verify the installation with `istioctl verify-install`
- Get the IstioOperator YAML for a configuration profile with `istioctl profile dump [profile_name]`
- Learn where to configure [global mesh settings](https://istio.io/latest/docs/reference/config/istio.mesh.v1alpha1/) and individual components (`pilot`, `ingressGatways`, `egressGateways`)

Here's an example of an IstioOperator resource that shows where (and how) to configure different components:

```yaml
apiVersion: install.istio.io/v1alpha1
# Reference: https://istio.io/latest/docs/reference/config/istio.operator.v1alpha1/
kind: IstioOperator 
spec:
  # Configuration profile used as base for installation
  # Other settings you can configure on this level:
  # namespace, hub, revision, tag
  profile: demo

  # Mesh configuration settings: https://istio.io/latest/docs/reference/config/istio.mesh.v1alpha1/
  meshConfig: 
    accessLogFile: /dev/stdout

  # Individual components you can configure: https://istio.io/latest/docs/reference/config/istio.operator.v1alpha1/#IstioComponentSetSpec
  # Includes base, pilot, cni, ztunnel, ingressGatways, egressGatways, istiodRemote
  components:
    # pilot: ..
    # cni: ...
    egressGateways:
    # There can be more than 1 egress gateway - note that to customize a gateway
    # that already exists in the profile (e.g. demo in this case), you need to use the default names
      - name: istio-egressgateway
        enabled: false
    ingressGateways:
        # Disable the default ingress gateway
      - name: istio-ingressgateway
        enabled: false
        # Enable a new ingress gateway
      - name: peters-gateway
        enabled: true
        namespace: custom-ns-name
        label:
          app: custom-label
        # Customize the k8s resources: https://istio.io/latest/docs/reference/config/istio.operator.v1alpha1/#KubernetesResourcesSpec
        k8s:
          resources:
            requests:
              cpu: 5m
              memory: 20Mi
```

## Resources

- [Installing with Istio CLI]( https://istio.io/latest/docs/setup/install/istioctl/)
- [Installing with Helm](https://istio.io/latest/docs/setup/install/helm/)
- [Customizing the installation](https://istio.io/latest/docs/setup/additional-setup/customize-installation/)
- [Customizing Kubernetes settings](https://istio.io/latest/docs/setup/additional-setup/customize-installation/#customize-kubernetes-settings)
- [Installing Gateways separately](https://istio.io/latest/docs/setup/additional-setup/gateway/)
- [IstioOperator Options](https://istio.io/latest/docs/reference/config/istio.operator.v1alpha1/)



## Session 2: Traffic management

[Streaming on October 3, 9:00 am PST / 12:00 pm EST / 6:00 pm CET](https://www.youtube.com/watch?v=Q-l1z3ejc8Q)

## Session 3: Resiliency and fault injection

[Streaming on October 4, 9:00 am PST / 12:00 pm EST / 6:00 pm CET](https://www.youtube.com/watch?v=df6A9PyhubQ)

## Session 4: Securing workloads

[Streaming on October 5, 8:00 am PST / 11:00 am EST / 5:00 pm CET](https://www.youtube.com/watch?v=uO-X1U1l23I)

## Session 5: Advanced scenarios

[Streaming on October 6, 9:00 am PST / 12:00 am EST / 6:00 pm CET](https://www.youtube.com/watch?v=Od7L-3tE9oA)