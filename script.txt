const btn_create = document.getElementById("btn-create");
const btn_close = document.getElementById("btn-close");
const qr_code = document.getElementById("qr-img")
const qr_code_container = document.querySelector(".qr-code-container")

const type_container = document.querySelectorAll(".type-container");
const forms = document.querySelectorAll(".form-container");

type_container[0].classList.add("active");
forms[0].classList.add("show");

type_container.forEach((type, idx) => {
    type.addEventListener("click", () => {
        type_container.forEach(c => c.classList.remove("active"));
        forms.forEach(f => f.classList.remove("show"));
        type.classList.add("active");
        forms[idx].classList.add("show");
        code_data()
    })
});

const text_input = document.getElementById("text-input");

btn_create.addEventListener("click", () => {
    let qr_value = code_data();
    qr_code.src = `https://api.qrserver.com/v1/create-qr-code/?size=400x400&data=${qr_value}`;
    show_QR();
})

btn_close.addEventListener("click", hide_QR);

function show_QR() {
    qr_code_container.classList.add("show");
    document.body.classList.add("overlay");
}

function hide_QR() {
    qr_code_container.classList.remove("show");
    document.body.classList.remove("overlay");
}
code_data()
function code_data() {
    let result;
    type_container.forEach((type, idx) => {
        if (type.classList.contains("active")) {
            result = form_function(type.dataset.type)
        }
    });
    return result;
}

function form_function(type) {
    let result;
    switch (type) {
        case "text": result = text_input.value; break;
        case "email": result = email(); break;
        case "phone": result = phone(); break;
        case "wifi": result = wifi(); break;
        case "contact": console.log("contact");
            break;
        case "facebook": console.log("facebook");
            break;
        case "twitter": console.log("twitter");
            break;
        case "whatsapp": console.log("whatsapp");
            break;
        case "sms": console.log("sms");
            break;
        case "instagram": console.log("instagram");
            break;
        case "linkedin": console.log("linkedin");
            break;
        case "website": console.log("website");
            break;
        case "gpay": console.log("gpay");
            break;
        case "bhim": console.log("bhim");
            break;
        case "phonepe": console.log("phonepe");
            break;
        case "youtube": console.log("youtube");
            break;
        default: console.log("Error Occurred");
    }

    return result;
}

function phone() {
    const phone_input = document.getElementById("phone");

    return `tel:${phone_input.value}`;
}

function email() {
    const email_input = document.getElementById("e-mail").value;
    const subject_input = document.getElementById("subject").value;
    const content_input = document.getElementById("content").value;

    console.log(content_input)
    return `mailto:${email_input}?subject=${subject_input}&body=${content_input}`;
}

function wifi() {

    const secs = Array.from(document.querySelectorAll(".sec"));
    var security;

    secs.forEach(s => {
        s.addEventListener("click", () => {
            secs.forEach(s => s.classList.remove("active"));
            s.classList.add("active");
        })
    })


    const hiddens = Array.from(document.querySelectorAll(".hide"));
    var hidden;
    hiddens.forEach(s => {
        s.addEventListener("click", () => {
            hiddens.forEach(s => s.classList.remove("active"));
            s.classList.add("active");
        })
    })
    btn_create.addEventListener("click", () => {
        const password = document.getElementById("network-password").value;
        const network_name_input = document.getElementById("network-name").value;

        security = secs.find(s => (s.classList.contains("active"))).dataset.security;
        hidden = hiddens.find(s => (s.classList.contains("active"))).dataset.hidden;


    })
    console.log(`WIFI:S:${network_name_input};T:${security};P:${password};H:${hidden};`);
    return `WIFI:S:${network_name_input};T:${security};P:${password};H:${hidden};`;
    // return `WIFI:S:JioFiber-5G;T:WPA;P:@01112021;H:blank;`;
}