<script>
    import { toasts,ToastContainer, FlatToast}  from "svelte-toasts";

    export let data;
    let mail = 'abhinav14863@gmail.com';
    let id = '' ;
    let send = () => {
        var text = document.getElementById('text').value.split('\n');
        var body = text.join('%0D%0A');
        let bod = document.getElementById("text").value;
        let email = id;
        let subject = data.post.title;
        window.location = "mailto:" + email + "?subject=" + subject + "&body=" + body;
        
    }
    const showToast = () => {
    const toast = toasts.add({
      title: 'Success',
      description: 'Copied to Clipboard',
      duration: 3000, // 0 or negative to avoid auto-remove
      placement: 'bottom-right',
      type: 'info',
      theme: 'dark',
      placement: 'bottom-right',
			showProgress: true,
      type: 'success',
      theme: 'dark',
      onClick: () => {},
      onRemove: () => {},
      // component: BootstrapToast, // allows to override toast component/template per toast
    });

  };

    const handlecopy = () => {
        let postdata=  data.post.content
        navigator.clipboard.writeText(postdata)
        // alert("copied to clipboard")
        showToast()
        setTimeout(() => setCopied(""), 5000);
    };


</script> 

<br/>
<div class="flex items-center justify-center gap-5 md:gap-10">
    <div class="">
        <input bind:value={id}  type="text" id="email" class="border text-gray-900 text-sm md:text-lg rounded-lg focus:ring-primary-500 focus:border-primary-500 block w-full px-6 py-4 bg-neutral-100 dark:bg-gray-900 border-primary-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-primary-500 dark:focus:border-primary-500" placeholder="example@mail.com" required>
    </div> 
    
    <div on:click={send} class="relative inline-flex items-center justify-start py-3 pl-4 pr-12 overflow-hidden font-semibold text-primary-400 transition-all duration-150 ease-in-out rounded hover:pl-10 hover:pr-6 bg-gray-900` group">
        <span class="absolute bottom-0 left-0 w-full h-1 transition-all duration-150 ease-in-out bg-indigo-600 group-hover:h-full"></span>
        <span class="absolute right-0 pr-4 duration-200 ease-out group-hover:translate-x-12">
            <svg class="w-5 h-5 text-green-400" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3"></path></svg>
        </span>
        <span class="absolute left-0 pl-2.5 -translate-x-12 group-hover:translate-x-0 ease-out duration-200">
            <svg class="w-5 h-5 text-green-400" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3"></path></svg>
        </span>
        <span class="relative text-sm sm:text-lg w-full text-left transition-colors duration-200 ease-in-out group-hover:text-white">Send Mail</span>
    </div>
    
</div>

<button class="mt-10 rounded-md text-lg text-white w-[12rem] m-auto center dark:bg-white/10 shadow-[inset_10px_-50px_94px_0_rgb(199,199,199,0.2)] backdrop-blur flex justify-center items-center cursor-pointer hover:text-slate-300 transition hover:scale-x-[1.01] bg-slate-900" on:click={handlecopy}>
    Copy to clipboard🗒️
</button> 
<ToastContainer let:data={data}>
    <FlatToast {data}  />
</ToastContainer>
<h1 class="sm:text-4xl text-3xl text-gray-800 dark:text-white mt-10 mb-5 text-center">{data.post.title}</h1>
<textarea id="text" cols="100" class="mx-auto max-w-full block text-gray-600 dark:text-white  text-lg sm:text-2xl sm:leading-loose leading-relaxed p-6 h-screen bg-neutral-100 dark:bg-gray-900">{data.post.content}</textarea>
