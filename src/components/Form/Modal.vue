<template>
  <div
    class="modal fade"
    id="dataModal"
    tabindex="-1"
    aria-labelledby="dataModalLabel"
    aria-hidden="true"
  >
    <div class="container">
      <div class="modal-dialog">
        <div class="modal-content">
          <div>
            <div class="modal-header">
              <h5 class="modal-title" id="dataModalLabel">
                Vehicle information
              </h5>
              <button
                type="button"
                class="btn-close"
                data-bs-dismiss="modal"
                aria-label="Close"
              ></button>
            </div>
            <hr style="border: 1px dashed #d1d1d1" />
            <div class="modal-body">
              <div class="pb-2">
                <p>
                  <span class="fw-bold me-2">Vehicle ID:</span>
                  {{ results.id }}
                </p>
              </div>
              <div class="col-12 pb-2">
                <h4>You've entered the following informations:</h4>
              </div>
              <div class="col-12 py-2 ps-3 padding-0">
                <p>
                  <span class="fw-bold me-2 width-100"
                    >Name of the vehicle:</span
                  >
                  {{ results.vehicleName }}
                </p>
              </div>
              <div class="col-12 py-2 ps-3 padding-0">
                <p>
                  <span class="fw-bold me-2 width-100"
                    >Type of the vehicle:</span
                  >
                  {{ results.vehicleType }}
                </p>
              </div>
              <div class="col-12 py-2 ps-3 padding-0">
                <p>
                  <span class="fw-bold me- width-1002"
                    >Model of the vehicle:</span
                  >
                  <span class="text-capitalize ms-1">{{
                    results.vehicleModel != ""
                      ? results.vehicleModel
                      : "Unknown"
                  }}</span>
                </p>
              </div>
              <hr style="border: 1px dashed #d1d1d1" />
              <div class="col-12 pt-4 padding-0">
                <h4>License plate & Registration:</h4>
              </div>
              <div class="col-12 pt-3 pb-1 ps-3 padding-0">
                <p>
                  <span class="fw-bold me-2">License plate number: </span>
                  <span class="text-uppercase">
                    {{ results.licensePlate }}</span
                  >
                </p>
              </div>
              <div class="col-12 py-2 ps-3 padding-0">
                <p>
                  <span class="fw-bold me-2 width-100"
                    >Your last registration date is:</span
                  >
                  {{ results.registrationDate }}
                </p>
              </div>
              <div class="col-12 py-2 ps-3 padding-0">
                <p>
                  <span class="fw-bold me-2 width-100"
                    >New registration submission on:</span
                  >
                  {{ results.registrationSubmission }}
                </p>
              </div>
            </div>
            <hr style="border: 1px dashed #d1d1d1" />
            <div class="modal-footer">
              <button
                type="button"
                class="btn btn-submit me-4"
                data-bs-dismiss="modal"
              >
                Close
              </button>
              <button type="button" @click="downloadPDF" class="btn btn-print">
                Generate PDF
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import jsPDF from "jspdf";
import html2canvas from "html2canvas";

export default {
  name: "Modal",
  props: ["results"],
  methods: {
    downloadPDF() {
      window.html2canvas = html2canvas;

      let doc = new jsPDF("p", "pt", "a4");

      doc.setFontSize(8);

      doc.html(document.querySelector(".modal-content"), {
        callback: (pdf) => {
          pdf.save("vehicleinfo.pdf");
        },
      });
    },
  },
};
</script>

<style scoped>
.btn-submit {
  background-color: #42505c;
  color: #fff;
  padding: 14px 30px;
  border-radius: 2px;
  font-weight: bold;
}

.btn-submit:hover {
  background-color: rgba(66, 80, 92, 0.7);
  color: #fff;
}

.btn-print {
  background-color: rgba(251, 191, 36, 1);
  color: #fff;
  padding: 14px 30px;
  border-radius: 2px;
  font-weight: bold;
}

.btn-print:hover {
  background-color: rgba(251, 191, 36, 0.8);
  color: #fff;
}
.modal-dialog {
  min-width: 960px;
}
.modal-header {
  border: none;
}
.modal-title {
  color: #42505c;
  font-size: 35px;
  font-weight: bold;
}
.modal-content {
  padding: 20px 40px;
}
.modal-footer {
  border: none;
}

@media only screen and (max-width: 810px) {
  .modal-content {
    width: 73%;
  }
}

@media only screen and (max-width: 420px) {
  .modal-content {
    width: 39%;
  }
  .modal-title {
    font-size: 30px;
  }
  h4 {
    font-size: 1.1rem;
  }
  .btn-submit {
    margin: 0 !important;
  }
  .btn-print {
    display: none;
  }
}
@media only screen and (max-width: 375px) {
  .modal-content {
    width: 35%;
  }

  .padding-0 {
    padding-left: 0 !important;
  }
}
</style>
