# pagination_Nextjs

## Pagination, If need to pass query(page_Number) to API

#### initialize the page, get the page value from url and set to state
```
const [pageSelected, setPageSelected] = useState(1);
  useEffect(() => {
    if(!router.query.page){
      router.push({ pathname: router.pathname, query: { page: 1  } });     
    }else{
      setPageSelected(router.query.page);     
    }
  },[]);
  ```
  
  #### update the url when state updated
  ```  
  useEffect(() => {
    router.push({ pathname: router.pathname, query: { page: pageSelected  } });     
  },[pageSelected]);
  ```
  
  #### update the state when page changes
  ```  
  const onChange = (e) => {         
    setPageSelected(e);
  }

  ```
  
  #### Pagination component
  ```
   <Pagination current={Number(pageSelected)} total={trending?.pager?.total_items} onChange={onChange} />  
  ```




## Pagination, If don't need to pass query to API

```

import React,{ useState, useEffect } from 'react'
import { Pagination as Pagi } from 'antd';
import Post from './Post';
import { useRouter } from 'next/router';

const PER_PAGE_LIMIT   = 5;

export default function Pagination({ posts }) {
  const [page, setPage] = useState(null);
  const [pageData, setPageData] = useState([]);

  const router = useRouter();

  useEffect(()=>{
    if(!router.query.page){
      setPage(1);
    }else{
      setPage(router.query.page)
    }
  },[])

  useEffect(()=>{
      router.push({ pathname: router.pathname, query: { page: page  } });   
    
    const upperBond = page*PER_PAGE_LIMIT;
    const lowerBond = upperBond - PER_PAGE_LIMIT;
    
    const tempPageData = posts?.slice(lowerBond,upperBond);
    
    setPageData(tempPageData);
    
  },[page])
  
  console.log("PER_PAGE : ",pageData);

  const onPageChange = (e)=>{    
      setPageData([]);
      setPage(e);
  }

  console.log("PAGE : ",page);

  return (
    <div>
      <h2> POSTS </h2>

      {pageData?.map((post, ind) => {
        return <Post post={post} key={ind} />.    // returns card
      })}

      <br />
        <Pagi current={+page} total={posts?.length/PER_PAGE_LIMIT} defaultPageSize={1} onChange={onPageChange}/>
      </div>
  )
}


```
