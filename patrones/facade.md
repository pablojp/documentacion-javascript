# Patrón Façade (Fachada)

Este es un patrón de diseño estructural que se usa ampliamente en las bibliotecas de JavaScript. Se utiliza para proporcionar una interfaz unificada y más simple, orientada al público para facilitar su uso que protege de las complejidades de sus subsistemas o subclases consistentes.

El uso de este patrón es muy común en bibliotecas como jQuery.

En este ejemplo, creamos una API pública con la clase ComplaintRegistry. Expone solo un método para ser utilizado por el cliente, es decir registerComplaint. Se maneja internamente crear instancias de objetos de obligados, ya sea ProductComplainto ServiceComplaintbasados en el argumento de tipo. También maneja todas las demás funcionalidades complejas, como generar una ID única, almacenar la queja en la memoria, etc. Pero, todas estas complejidades se ocultan utilizando el patrón de fachada.

```javascript
let currentId = 0;

class ComplaintRegistry {
  registerComplaint(customer, type, details) {
    const id = ComplaintRegistry._uniqueIdGenerator();
    let registry;
    if (type === 'service') {
      registry = new ServiceComplaints();
    } else {
      registry = new ProductComplaints();
    }
    return registry.addComplaint({ id, customer, details });
  }

  static _uniqueIdGenerator() {
    return ++currentId;
  }
}

class Complaints {
  constructor() {
    this.complaints = [];
  }

  addComplaint(complaint) {
    this.complaints.push(complaint);
    return this.replyMessage(complaint);
  }

  getComplaint(id) {
    return this.complaints.find(complaint => complaint.id === id);
  }

  replyMessage(complaint) {}
}

class ProductComplaints extends Complaints {
  constructor() {
    super();
    if (ProductComplaints.exists) {
      return ProductComplaints.instance;
    }
    ProductComplaints.instance = this;
    ProductComplaints.exists = true;
    return this;
  }

  replyMessage({ id, customer, details }) {
    return `Complaint No. ${id} reported by ${customer} regarding ${details} have been filed with the Products Complaint Department. Replacement/Repairment of the product as per terms and conditions will be carried out soon.`;
  }
}

class ServiceComplaints extends Complaints {
  constructor() {
    super();
    if (ServiceComplaints.exists) {
      return ServiceComplaints.instance;
    }
    ServiceComplaints.instance = this;
    ServiceComplaints.exists = true;
    return this;
  }

  replyMessage({ id, customer, details }) {
    return `Complaint No. ${id} reported by ${customer} regarding ${details} have been filed with the Service Complaint Department. The issue will be resolved or the purchase will be refunded as per terms and conditions.`;
  }
}

// usage
const registry = new ComplaintRegistry();

const reportService = registry.registerComplaint('Martha', 'service', 'availability');
// 'Complaint No. 1 reported by Martha regarding availability have been filed with the Service Complaint Department. The issue will be resolved or the purchase will be refunded as per terms and conditions.'

const reportProduct = registry.registerComplaint('Jane', 'product', 'faded color');
// 'Complaint No. 2 reported by Jane regarding faded color have been filed with the Products Complaint Department. Replacement/Repairment of the product as per terms and conditions will be carried out soon.'
```
